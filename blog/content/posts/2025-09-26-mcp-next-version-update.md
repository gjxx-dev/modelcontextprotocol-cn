---
title: "下一个 MCP 协议版本的更新"
date: 2025-09-26T10:00:00-08:00
draft: false
tags: ["mcp", "protocol", "roadmap", "community"]
author: "David Soria Parra"
description: "关于 Model Context Protocol 规范下一个版本的时间表和优先级的更新"
---

## 发布时间表

Model Context Protocol 规范的下一个版本将于 **2025 年 11 月 25 日** 发布，发布候选版本 (RC) 将于 **2025 年 11 月 11 日** 提供。

我们构建了一个 14 天的 RC 验证窗口，以便客户端实现者和 SDK 维护者可以彻底测试协议更改。这种方法为我们提供了交付关键改进所需的专注时间，同时将我们的[新治理模式](https://modelcontextprotocol.io/community/governance)应用于流程。

## 夏季进展

我们上一个规范于 2025 年 6 月 18 日发布，专注于结构化工具输出、基于 OAuth 的授权、服务器发起的用户交互的引出，以及改进的安全最佳实践。

从那时起，我们专注于为 MCP 生态系统建立额外的基礎：

### 正式治理结构

我们建立了 MCP 的[正式治理模式](https://modelcontextprotocol.io/community/governance)，包括定义的角色和决策机制。我们还开发了[规范增强提案 (SEP)](https://modelcontextprotocol.io/community/sep-guidelines) 流程，为贡献规范更改提供清晰的指南。

我们的目标是透明——使决策程序对每个人都清晰和可访问。像任何服务于快速演变社区的新系统一样，我们的治理模式仍在寻找立足点。随着协议和社区的持续增长，我们正在积极完善它。

### 工作组

我们启动了[工作组和兴趣组](https://modelcontextprotocol.io/community/working-interest-groups) 以促进社区协作。这些组服务于多个目的：

- 为新贡献者提供清晰的入口点
- 授权社区成员在他们的专业领域领导倡议
- 在生态系统中分配所有权，而不是集中在核心维护者中

我们正在开发治理结构，这些结构将授予这些组更大的决策和实施自主权。这种分布式方法确保协议能够增长以满足社区需求，同时在不同领域保持质量和一致性。

### 注册表开发

9 月，我们[推出了 MCP 注册表预览](https://blog.modelcontextprotocol.io/posts/2025-09-08-mcp-registry-preview/)——一个用于索引和发现 MCP 服务器的开放目录和 API。注册表作为可用 MCP 服务器的单一真相来源，支持组织可以为他们的特定需求定制的公共和私有子注册表。

构建 MCP 注册表是一个真正的社区努力。任何 MCP 客户端都可以通过原生 API 或第三方注册表聚合器消费注册表内容，使用户更容易发现和集成 MCP 服务器到他们的 AI 工作流中。

## 下一个版本的优先领域

随着治理和基础设施基础到位，我们专注于工作组确定的五个关键协议改进。

### 异步操作

目前，MCP 围绕主要是同步操作构建——当您调用工具时，一切都会停止并等待它完成。这对快速任务很有效，但对于需要几分钟或几小时的操作呢？

代理工作组正在添加异步支持，允许服务器启动长时间运行的任务，而客户端可以稍后检查结果。您可以在 [SEP-1391](https://github.com/modelcontextprotocol/modelcontextprotocol/issues/1391) 中关注进展。

### 无状态性和可扩展性

随着组织在企业规模部署 MCP 服务器，我们看到新的需求出现。当前实现通常需要在请求之间记住事物，这使得跨多个服务器实例的水平扩展具有挑战性。

虽然 [Streamable HTTP](https://modelcontextprotocol.io/specification/2025-03-26/basic/transports#streamable-http) 提供了一些无状态支持，但在服务器启动和会话处理方面仍然存在痛点。传输工作组正在平滑这些粗糙边缘，使在生产中运行 MCP 服务器更容易，同时为想要更复杂的有状态功能的团队保持简单的升级路径。

### 服务器身份

今天，如果您想知道 MCP 服务器能做什么，您必须首先连接到它。这使得客户端难以浏览可用服务器，或像我们的注册表这样的系统难以自动编目功能。

我们通过让服务器通过 [`.well-known` URLs](https://en.wikipedia.org/wiki/Well-known_URI) 广告自己来解决这个问题——这是一个为提供元数据而建立的标准。将其视为服务器的名片，任何人都可以在不敲门的情况下阅读。这将使每个 MCP 消费者的发现变得更加直观。

### 官方扩展

随着 MCP 的增长，我们注意到特定行业和用例的模式正在出现——有价值的实现，不一定属于核心协议规范。

与其让每个人重新发明轮子，我们正式认可和记录最受欢迎的协议扩展。这个经过验证的模式集合将为在医疗保健、金融或教育等专业领域构建的开发者提供坚实起点，而不是从头构建每个自定义集成。

### SDK 支持标准化

今天选择 MCP SDK 可能具有挑战性——很难衡量您将获得的规范合规性水平或支持水平。有些 SDK 更新速度极快，而其他可能在功能方面落后。

我们正在引入一个清晰的 SDK 分层系统。在提交依赖之前，您将确切知道您在注册什么，基于规范合规速度、维护响应性和功能完整性等因素。

## 贡献者呼吁

MCP 只有在背后的社区一样强大。无论您是热衷于构建 SDK 的个人开发者，还是希望投资生态系统的公司，我们在几个关键领域需要您的帮助。

### SDK 维护

- [**TypeScript SDK**](https://github.com/modelcontextprotocol/typescript-sdk) - 需要额外的维护者进行功能开发和错误修复
- [**Swift SDK**](https://github.com/modelcontextprotocol/swift-sdk) - 需要关注 Apple 生态系统支持
- [其他语言 SDK](https://modelcontextprotocol.io/docs/sdk) 欢迎持续贡献

### 工具

- [**Inspector**](https://github.com/modelcontextprotocol/inspector) - 为 MCP 服务器开发者开发和维护调试工具
- [**Registry**](https://github.com/modelcontextprotocol/registry) - 后端 API 和 CLI 开发；**特别欢迎 Go 专业知识**

## 来自客户端开发者的输入

我们经常谈论 MCP 服务器，但客户端同样重要——它们是将用户连接到整个 MCP 生态系统的桥梁。如果您正在构建 MCP 客户端，您正在从独特的角度看待协议，我们需要将这种视角嵌入协议设计中。

您在实现挑战、性能瓶颈和用户需求方面的实际经验直接塑造了协议下一步的方向。无论是关于现有功能的反馈，还是关于简化开发者体验的想法，我们都想听到您的声音。

加入我们在 [MCP Discord](https://modelcontextprotocol.io/community/communication) 中 `#client-implementors` 工作组频道的讨论。

## 前瞻

随着治理结构和工作组到位，我们更好地定位于高效处理主要协议改进，同时确保每个人在过程中都有发言权。我们这个夏天完成的基础工作为我们提供了构建的坚实基础。

11 月即将推出的改进——异步操作、更好的可扩展性、服务器发现和标准化扩展——将帮助 MCP 成为生产 AI 集成的更强大骨干。但我们无法独自完成。

MCP 的力量一直是它是**由社区为社区构建的开放协议**。我们很高兴继续一起构建它。

感谢您持续的支持，我们期待很快分享更多。
