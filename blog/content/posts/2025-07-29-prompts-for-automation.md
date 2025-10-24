+++
date = '2025-08-04T18:00:00+01:00'
publishDate = '2025-08-04T18:00:00+01:00'
draft = false
title = 'MCP 提示词：构建工作流自动化'
author = 'Inna Harper (Core Maintainer)'
tags = ['automation', 'mcp', 'prompts', 'tutorial']
+++

[MCP (Model Context Protocol)](https://modelcontextprotocol.io/specification/2025-06-18) 提示词通过将 AI 能力与结构化数据访问相结合来实现工作流自动化。本文通过一个实际示例演示了如何使用 MCP 的[提示词](https://modelcontextprotocol.io/specification/2025-06-18/server/prompts)和[资源模板](https://modelcontextprotocol.io/specification/2025-06-18/server/resources#resource-templates)来构建自动化。

本指南演示了 MCP 提示词如何自动化重复性工作流。无论您是对 MCP 生态系统感兴趣，还是只是想利用 AI 进行工作流自动化，您都将通过一个具体的餐食规划示例学习如何构建实用的自动化。不需要事先了解 MCP——我们将在深入实现之前介绍基础知识。

## 问题：耗时的重复性任务

每个人都有一些重复性任务，这些任务会占用他们的生产时间。常见示例包括应用代码审查反馈、生成每周报告、更新文档或创建样板代码。这些任务并不复杂——它们遵循可预测的模式——但它们繁琐且耗时。[MCP 提示词](https://modelcontextprotocol.io/specification/2025-06-18/server/prompts)正是为了帮助自动化此类工作而设计的。

MCP 提示词不仅仅是命令快捷方式。它们是构建工作流自动化的原语，将脚本的灵活性与现代 AI 系统的智能相结合。本文探讨了如何使用 MCP 的提示词系统、资源模板和模块化服务器来构建自动化。我将通过我构建的一个餐食规划自动化来演示这些概念，但这些模式广泛适用于任何结构化的重复性工作流。

## 示例：自动化每周餐食规划

我需要解决一个反复出现的问题：按菜系规划每周餐食以高效管理食材。手动过程涉及选择菜系、选择菜肴、列出食材、购物和组织食谱——这些重复步骤每周都要花费大量时间。

所以我决定使用 MCP！通过自动化这些步骤，我可以将整个工作流简化为选择菜系并接收完整的餐食计划和购物清单。（任何支持 MCP 提示词的客户端都应该可以工作！）

1. **选择提示词**

   <img
   src="/posts/images/prompts-list.png"
   alt="MCP 提示词列表显示可用的自动化命令"
   />

2. **从下拉菜单中选择菜系**
   <img
     src="/posts/images/prompts-suggestions.png"
     alt="下拉菜单显示用户输入时的菜系列表建议"
   />
3. **完成！**
   系统生成餐食计划、购物清单，甚至打印购物清单和食谱。

<img
    src="/posts/images/prompts-final-result.png"
    alt="最终生成的餐食计划和购物清单输出"
  />

这里我们主要关注带有提示词和资源的食谱服务器。您可以在[这里找到打印服务器示例](https://github.com/ihrpr/mcp-server-tiny-print)（它适用于特定的热敏打印机型号，但您可以轻松将其替换为电子邮件、Notion 或任何其他输出方法）。独立服务器的美妙之处在于您可以混合搭配不同的能力。

## 核心组件

让我们深入了解使这种自动化成为可能的三个组件：[提示词](https://modelcontextprotocol.io/specification/2025-06-18/server/prompts)、[资源](https://modelcontextprotocol.io/specification/2025-06-18/server/resources)和[完成](https://modelcontextprotocol.io/specification/2025-06-18/server/utilities/completion)。我将展示每个组件的概念工作原理，然后我们一起实现它们。

### 1. Resource Templates

In MCP, [static resources](https://modelcontextprotocol.io/specification/2025-06-18/server/resources#resource-types) represent specific pieces of content with unique URIs—like `file://recipes/italian.md` or `file://recipes/mexican.md`. While straightforward, this approach doesn't scale well. If you have recipes for 20 cuisines, you'd need to define 20 separate resources, each with its own URI and metadata.

[Resource templates](https://modelcontextprotocol.io/specification/2025-06-18/server/resources#resource-templates) solve this through URI patterns with parameters, transforming static resource definitions into dynamic content providers.

For example, a template like `file://recipes/{cuisine}.md` might represent a set of resources like these:

- `file://recipes/italian.md` returns Italian recipes
- `file://recipes/mexican.md` returns Mexican recipes

This pattern extends beyond simple filtering. You can create templates for:

- Hierarchical data: `file://docs/{category}/{topic}`
- Git repository content: `git://repo/{branch}/path/{file}`
- Web resources: `https://api.example.com/users/{userId}/data`
- Query parameters: `https://example.com/{collection}?type={filter}`

For more details on URI schemes and resource templates, see the [MCP Resource specification](https://modelcontextprotocol.io/specification/2025-06-18/server/resources#resource-templates).

### 2. Completions

Nobody remembers exact parameter values. Is it "italian" or "Italian" or "it"? [Completions](https://modelcontextprotocol.io/specification/2025-06-18/server/utilities/completion) bridge this gap by providing suggestions as users type, creating an interface that feels intuitive rather than restrictive.

Different MCP clients present completions differently:

- VS Code shows a filterable dropdown
- Command-line tools might use fuzzy matching
- Web interfaces could provide rich previews

But the underlying data comes from your server, maintaining consistency across all clients.

### 3. Prompts: Commands That Evolve With Context

[Prompts](https://modelcontextprotocol.io/specification/2025-06-18/server/prompts) are the entry points to your automation. They define what commands are available and can range from simple text instructions to rich, context-aware operations.

Let's see how prompts can evolve to handle increasingly sophisticated use cases:

**Basic prompt: Static instruction**

```
"Create a meal plan for a week"
```

This works, but it's generic. The AI will create a meal plan based on general knowledge.

**Adding parameters: Dynamic customization**

```
"Create a meal plan for a week using {cuisine} cuisine"
```

现在用户可以指定意大利菜、墨西哥菜或其他任何菜系。提示词会根据用户输入进行调整，但仍然依赖于 AI 对这些菜系的一般知识。

**包含资源：您的数据**

提示词可以包含资源，以添加超出简单文本指令的上下文数据。当您需要 AI 使用您的特定上下文而不是一般知识时，这一点至关重要。

在我的餐食规划示例中，我不想要通用食谱——我希望 AI 使用**我**的经过测试的食谱收藏，这些是我知道我喜欢的食谱。复杂提示词通过将提示词文本与嵌入资源捆绑在一起使这成为可能。

工作原理如下：

1. **用户选择带有参数的提示词**（例如，"plan-meals"，cuisine="italian"）
2. **服务器返回**指令文本和资源引用
3. **客户端决定如何处理资源** - 应用程序可能选择使用嵌入或关键词搜索选择数据子集，或直接将原始数据传递给模型
4. **AI 接收上下文**并生成响应

在我的示例中，VS Code 将整个资源附加到提示词，这对这个用例非常有效。AI 在规划意大利周时可以访问我所有的意大利食谱，确保它只建议我实际有食谱的菜肴。

与简单提示词的关键区别：不是询问"规划意大利餐食"并获得通用建议，而是 AI 使用您实际的食谱收藏、饮食偏好和限制。

<img
    src="/posts/images/prompts-rendered-prompt.png"
    alt="VS Code 显示带有附加食谱资源的渲染提示词"
  />

我们一直在使用的食谱资源是**嵌入资源**，它们具有来自服务器的内联内容。根据[MCP 规范](https://modelcontextprotocol.io/specification/2025-06-18/server/prompts#data-types)，提示词还可以包含其他数据类型。

这启用了超出我们基于文本的食谱的高级用例，例如带有截图的设计审查提示词或语音转录服务。

## 构建食谱服务器

让我们实现一个完整的 MCP 服务器，将我们讨论的所有概念结合起来。我们将从服务器设置开始，然后实现每个功能。

### 先决条件

在深入代码之前，请确保您有：

1. **Node.js**（v18 或更高版本）和 npm 已安装
2. **MCP SDK** 已安装：
   ```bash
   npm install @modelcontextprotocol/sdk
   ```
3. **支持提示词和资源的 MCP 兼容客户端**，如带有 MCP 扩展的 VS Code

在本教程中，我将使用 TypeScript SDK，但 MCP 也支持 Python 和其他语言。

### 服务器设置和功能

首先，让我们创建我们的 MCP 服务器：

```typescript
const server = new McpServer({
  name: "favorite-recipes",
  version: "1.0.0",
});

async function main() {
  const transport = new StdioServerTransport();
  await server.connect(transport);
}

main().catch((error) => {
  console.error("Server error:", error);
  process.exit(1);
});
```

### 实现资源

接下来，让我们注册一个带有完成的资源模板。

```typescript
server.registerResource(
  "recipes",
  new ResourceTemplate("file://recipes/{cuisine}", {
    list: undefined,
    complete: {
      cuisine: (value) => {
        return CUISINES.filter((cuisine) => cuisine.startsWith(value));
      },
    },
  }),
  {
    title: "Cuisine-Specific Recipes",
    description: "Traditional recipes organized by cuisine",
  },
  async (uri, variables, _extra) => {
    const cuisine = variables.cuisine as string;

    if (!CUISINES.includes(cuisine)) {
      throw new Error(`Unknown cuisine: ${cuisine}`);
    }

    const content = formatRecipesAsMarkdown(cuisine);
    return {
      contents: [
        {
          uri: uri.href,
          mimeType: "text/markdown",
          text: content,
        },
      ],
    };
  },
);
```

### 实现提示词

最后，让我们注册提示词，它也有完成：

```typescript
server.registerPrompt(
  "weekly-meal-planner",
  {
    title: "Weekly Meal Planner",
    description:
      "Create a weekly meal plan and grocery shopping list from cuisine-specific recipes",
    argsSchema: {
      cuisine: completable(z.string(), (value) => {
        return CUISINES.filter((cuisine) => cuisine.startsWith(value));
      }),
    },
  },
  async ({ cuisine }) => {
    const resourceUri = `file://recipes/${cuisine}`;
    const recipeContent = formatRecipesAsMarkdown(cuisine);

    return {
      title: `Weekly Meal Planner - ${cuisine} Cuisine`,
      description: `Weekly meal planner for ${cuisine} cuisine`,
      messages: [
        {
          role: "user",
          content: {
            type: "text",
            text: `Plan cooking for the week. I've attached the recipes from ${cuisine} cuisine.

Please create:
1. A 7-day meal plan using these recipes
2. An optimized grocery shopping list that minimizes waste by reusing ingredients across multiple recipes
3. Daily meal schedule with specific dishes for breakfast, lunch, and dinner
4. Preparation tips to make the week more efficient
5. Print Shopping list

Focus on ingredient overlap between recipes to reduce food waste.`,
          },
        },
        {
          role: "user",
          content: {
            type: "resource",
            resource: {
              uri: resourceUri,
              mimeType: "text/markdown",
              text: recipeContent,
            },
          },
        },
      ],
    };
  },
);
```

## 自己运行

[食谱服务器的完整代码在这里](https://github.com/ihrpr/mcp-server-fav-recipes)。

按照 VS Code 的[文档设置服务器](https://code.visualstudio.com/docs/copilot/chat/mcp-servers)。一旦在 VS Code 中设置了服务器，您就可以查看其状态、调试正在发生的事情，并在您的自动化上快速迭代。

在 VS Code 中设置服务器后，在聊天中输入 "/" 并选择提示词。

<img
    src="/posts/images/prompts-list.png"
    alt="MCP 提示词列表显示可用的自动化命令"
 />

## 扩展您的自动化

MCP 提示词开启了激动人心的自动化可能性：

- **提示词链**：按顺序执行多个提示词（规划餐食 → 生成购物清单 → 下单）
- **动态提示词**：根据可用资源或季节进行调整
- **跨服务器工作流**：协调多个 MCP 服务器进行复杂自动化
- **外部触发器**：通过 webhook 或计划激活提示词

在餐食规划中演示的模式适用于许多领域：

- 了解您代码库的文档生成
- 访问您数据源的报告创建
- 理解您项目结构的开发工作流
- 具有完整上下文的客户支持自动化

**关键要点：**

- MCP 提示词可以包含动态资源，为任务提供 AI 完整上下文
- 资源模板启用可扩展的内容服务而无需重复
- 模块化服务器架构让您可以混合搭配功能

## 总结

这个餐食规划自动化始于一个简单的愿望：避免每周重写购物清单。它演变为一个完整的系统，只需几次点击即可处理餐食规划、购物清单和食谱打印。

MCP 提示词提供了自动化重复性任务的实用工具。模块化架构意味着您可以从小开始——也许只是自动化您工作流的一部分——并根据需要扩展。无论您是在自动化文档、报告还是餐食规划，模式都是一样的：识别重复性任务，构建专注的自动化，让系统处理繁琐的部分。
