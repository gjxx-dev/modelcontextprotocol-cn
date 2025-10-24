+++
date = '2025-09-08T00:00:00Z'
title = '介绍 MCP 注册表'
author = 'David Soria Parra (Lead Maintainer), Adam Jones (Registry Maintainer), Tadas Antanavicius (Registry Maintainer), Toby Padilla (Registry Maintainer), Theodora Chu (MCP PM at Anthropic)'
tags = ['announcement', 'community']
+++

今天，我们推出 Model Context Protocol (MCP) 注册表——一个公开可用的 MCP 服务器的开放目录和 API，以提高可发现性和实现。通过标准化服务器的分布和发现方式，我们正在扩大它们的覆盖范围，同时使客户端更容易连接。

MCP 注册表现已提供预览。要开始使用：

- **添加您的服务器**，请按照我们的指南 [将服务器添加到 MCP 注册表](https://github.com/modelcontextprotocol/registry/blob/main/docs/guides/publishing/publish-server.md)（针对服务器维护者）
- **访问服务器数据**，请按照我们的指南 [访问 MCP 注册表数据](https://github.com/modelcontextprotocol/registry/blob/main/docs/guides/consuming/use-rest-api.md)（针对客户端维护者）

# MCP 服务器的单一真相来源

2025 年 3 月，我们分享了我们想要为 MCP 生态系统构建中央注册表的愿望。今天我们宣布，我们已推出 [https://registry.modelcontextprotocol.io](https://registry.modelcontextprotocol.io) 作为官方 MCP 注册表。作为 MCP 项目的一部分，MCP 注册表以及父级 [OpenAPI 规范](https://github.com/modelcontextprotocol/registry/blob/main/docs/reference/api/official-registry-api.md) 都是开源的——允许每个人构建兼容的子注册表。

我们的目标是标准化服务器的分布和发现方式，提供子注册表可以构建的基础真相来源。反过来，这将扩大服务器覆盖范围，并帮助客户端在 MCP 生态系统中更容易找到服务器。

## 公共和私有子注册表

在构建中央注册表时，对我们来说重要的是不要剥夺社区和公司已经构建的现有注册表。MCP 注册表作为公开可用 MCP 服务器的主要真相来源，组织可以选择基于自定义标准 [创建子注册表](https://github.com/modelcontextprotocol/registry/blob/main/docs/guides/consuming/use-rest-api.md#building-a-subregistry)。例如：

**公共子注册表** 如与每个 MCP 客户端关联的意见化 "MCP 市场" 可以自由地增强和改进它们从上游 MCP 注册表摄取的数据。每个 MCP 最终用户角色将有不同的需求，由 MCP 客户端市场以意见化的方式适当地服务他们的最终用户。

**私有子注册表** 将存在于具有严格隐私和安全要求的企業中，但 MCP 注册表为这些企業提供了一个单一的上游数据源，他们可以在此基础上构建。至少，我们的目标是与这些私有实现共享 API 模式，以便相关的 SDK 和工具可以在整个生态系统中共享。

在这两种情况下，MCP 注册表都是起点——它是 MCP 服务器维护者发布和维护其自我报告信息的集中位置，供这些下游消费者按摩并交付给他们的最终用户。

## 社区驱动的审核机制

MCP 注册表是一个官方 MCP 项目，由注册表工作组维护并采用宽松许可证。社区成员可以提交问题来标记违反 MCP [审核指南](https://github.com/modelcontextprotocol/registry/blob/main/docs/guides/administration/moderation-guidelines.md) 的服务器——例如包含垃圾邮件、恶意代码或冒充合法服务的服务器。然后注册表维护者可以将这些条目列入黑名单，并从公共访问中追溯性地移除它们。

# 开始使用

要开始使用：

- **添加您的服务器**，请按照我们的指南 [将服务器添加到 MCP 注册表](https://github.com/modelcontextprotocol/registry/blob/main/docs/guides/publishing/publish-server.md)（针对服务器维护者）
- **访问服务器数据**，请按照我们的指南 [访问 MCP 注册表数据](https://github.com/modelcontextprotocol/registry/blob/main/docs/guides/consuming/use-rest-api.md)（针对客户端维护者）

MCP 注册表的此预览旨在帮助我们在正式发布前改进用户体验，不提供数据持久性保证或其他保证。我们建议 MCP 采用者密切关注开发，因为在注册表正式发布前可能会发生重大更改。

随着我们继续开发注册表，我们鼓励在 [modelcontextprotocol/registry GitHub 仓库](https://github.com/modelcontextprotocol/registry) 上提供反馈和贡献：讨论、问题和拉取请求都欢迎。

# 感谢 MCP 社区

MCP 注册表从一开始就是一个协作努力，我们非常感谢更广泛的开发者社区的热情和支持。

2025 年 2 月，它始于一个草根项目，当时 MCP 创建者 [David Soria Parra](https://github.com/dsp-ant) 和 [Justin Spahr-Summers](https://github.com/jspahrsummers) 要求 [PulseMCP](https://www.pulsemcp.com/) 和 [Goose](https://block.github.io/goose/) 团队帮助构建一个集中的社区注册表。来自 [PulseMCP](https://www.pulsemcp.com/) 的注册表维护者 [Tadas Antanavicius](https://github.com/tadasant) 带头进行了最初的努力，与来自 [Block](https://block.xyz/) 的 [Alex Hancock](https://github.com/alexhancock) 合作。他们很快得到了来自 [GitHub](https://github.com/) 的 MCP 负责人注册表维护者 [Toby Padilla](https://github.com/toby) 的加入，最近，来自 [Anthropic](https://www.anthropic.com/) 的 [Adam Jones](https://github.com/domdomegg) 加入作为注册表维护者，推动项目走向今天的发布。[MCP 注册表开发的初始公告](https://github.com/modelcontextprotocol/registry/discussions/11) 列出了来自至少 9 家不同公司的 16 位贡献者。

Many others made crucial contributions to bring this project to life: [Radoslav Dimitrov](https://github.com/rdimitrov) from [Stacklok](https://stacklok.com/), [Avinash Sridhar](https://github.com/sridharavinash) from [GitHub](https://github.com/), [Connor Peet](https://github.com/connor4312) from [VS Code](https://code.visualstudio.com/), [Joel Verhagen](https://github.com/joelverhagen) from [NuGet](https://www.nuget.org/), [Preeti Dewani](https://github.com/pree-dew) from [Last9](https://last9.io/), [Avish Porwal](https://github.com/Avish34) from [Microsoft](https://www.microsoft.com/), [Jonathan Hefner](https://github.com/jonathanhefner), and many Anthropic and GitHub employees that provided code reviews and development support. We are also grateful to everyone on the [Registry's contributors log](https://github.com/modelcontextprotocol/registry/graphs/contributors) and those who participated in [discussions and issues](https://github.com/modelcontextprotocol/registry).

We deeply appreciate everyone investing in this foundational open source infrastructure. Together, we're helping developers and organizations worldwide to build more reliable, context-aware AI applications. On behalf of the MCP community, thank you.
