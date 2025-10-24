+++
date = '2025-07-31T00:00:00Z'
title = '基业长青：MCP 的新治理模式'
author = 'David Soria Parra (Lead Maintainer)'
tags = ['announcement', 'governance', 'community']
+++

自 2024 年 11 月开源发布以来，Model Context Protocol 项目的发展速度超出了我们的想象。这是一个很好的问题，但随着增长而来的是成长的烦恼。我们现有的流程对小团队来说运作良好，但已经开始显示其局限性。

今天，我们迈出了重要的一步，以确保 MCP 能够继续发展和繁荣。我们正在引入一个正式的治理模式，旨在为开发过程带来清晰度，同时保留使 MCP 成功的协作式开源精神。

## 规范增强提案 (SEPs)

我们引入的第一个重大变化是[规范增强提案](https://modelcontextprotocol.io/community/sep-guidelines) (SEPs)。这将成为任何人提出对 MCP 更改的主要机制。SEPs 受到其他项目（如 [Python PEPs](https://peps.python.org/) 或 [Rust RFCs](https://github.com/rust-lang/rfcs)）的启发。我们旨在使建议对 Model Context Protocol 进行更改的过程尽可能简单：

1. 按照 [SEP 指南](https://modelcontextprotocol.io/community/sep-guidelines)，提交提案作为 [GitHub issue](https://github.com/modelcontextprotocol/modelcontextprotocol/issues) 来开始对话。
2. 我们的维护者和核心维护者定期审查提案并标记 SEPs 进行审查和赞助。您也可以在 [Discord](https://discord.gg/6CSzBmMkjX) 或 [GitHub](https://github.com/modelcontextprotocol/modelcontextprotocol) 上与贡献者合作。请参考 [`MAINTAINERS.md`](https://github.com/modelcontextprotocol/modelcontextprotocol/blob/main/MAINTAINERS.md) 获取当前活跃维护者及其重点领域的列表。
3. 与赞助者和 MCP 社区合作，将您的提案推进草稿、审查和实施阶段。

SEPs 为协议演化提供了清晰、文档化的路径，确保每个重大更改都经过社区的充分审查。

## 领导角色

新模式还建立了三种类型的领导角色，确保既专注于所有权又广泛的社区代表：

- **维护者** 管理特定组件，如 SDK、我们的文档和各个仓库。
- **核心维护者** 指导项目的整体方向和 MCP 规范的演化。
- **首席维护者** 作为最终决策者和确保项目的长期健康。

所有维护者组成 **MCP 指导小组**。为了确保对传入提案的结构化和及时审查，我们的核心和首席维护者将每两周举行一次会议，审查提交的 [SEPs](#specification-enhancement-proposals-seps)。会议记录和决定将始终公开。例如 [2025 年 7 月 23 日核心维护者会议的记录](https://github.com/modelcontextprotocol/modelcontextprotocol/issues/1061)。

## 参与其中

我们需要您的帮助来构建 MCP 的未来，每个人都欢迎加入这里。无论您是经验丰富的开源老手，还是只是好奇如何入门，我们的社区都有您的位置。

我们的许多维护者都是从单个小贡献开始的——有时只是修复一个拼写错误或提出一个深思熟虑的问题。每段旅程都有起点，我们很高兴帮助您迈出第一步。

- **新贡献者**：不确定从哪里开始？从帮助文档、修复错误或构建示例开始。每项贡献都很重要，我们在这里支持您。查看标记为 [`good first issue`](https://github.com/modelcontextprotocol/modelcontextprotocol/issues?q=is%3Aissue%20state%3Aopen%20label%3A%22good%20first%20issue%22) 的问题 - 它们非常适合入门，您会发现友好的面孔随时准备帮助。
- **SDK 开发者**：有喜欢的编程语言吗？随着 MCP 的增长，我们需要您的专业知识来构建和维护协议 SDK。您的作品可以赋能整个新社区使用 MCP。
- **文档编写者**：清晰、全面的[文档](https://modelcontextprotocol.io/introduction)是将一个好的项目变成伟大项目的关键。如果您喜欢解释事物或制作指南，您的贡献将帮助他人成功。
- **未来的维护者**：我们相信从内部培养我们的团队。成为维护者的道路始于一致的、高质量的贡献以及对项目成功的承诺。想象一下自己指导新贡献者并塑造 MCP 的未来。

无论您的背景或经验如何，您都属于这里。加入我们的 [Discord](https://discord.gg/6CSzBmMkjX) 与其他贡献者联系、提问并寻找指导。无论您是修复拼写错误还是提出对协议的重大更改，您的声音都受到重视，您的努力会产生影响。

有关所有详细信息，请参阅我们的完整[治理文档](https://modelcontextprotocol.io/community/governance)。

## 致谢

如果没有围绕 MCP 集结的令人难以置信的社区，这一切都不可能实现。从相信愿景的早期采用者，到构建 MCP 客户端和服务器的开发者，再到奉献时间和专业知识的维护者。每项贡献对于使 Model Context Protocol 成为今天的成功都至关重要。

You've helped us identify issues, improve documentation, build SDKs, create compelling examples, and push the boundaries of what's possible with platform integration. Your feedback, bug reports, feature requests, and code contributions have shaped MCP into something far better than we could have built alone.

As we embark on this next chapter with formal governance, we're more committed than ever to fostering the open, inclusive community that has made MCP thrive. Thank you for being part of this journey - we can't wait to see what we'll build together next.
