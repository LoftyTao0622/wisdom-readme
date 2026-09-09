<div align="center">

<sub>EVIDENCE FIRST · VISUAL BY DESIGN · BILINGUAL</sub>

# generate-readme

**把仓库事实组织成读得懂、跑得通、值得信任的 README。**

An evidence-led README authoring skill for AI coding assistants.

[中文说明](./README.zh-CN.md) · [English guide](./README.en.md)

</div>

> 先让读者知道这是什么，再让他看到证据，最后给出一次成功的行动。

## 30 秒了解

`generate-readme` 面向需要创建、重写、审计或本地化 README 的维护者。它把仓库扫描、事实核对、结构选择和新手验证串成一条工作流，并根据项目性格选择简约、产品、编辑或参考型阅读体验。

```mermaid
flowchart LR
    A[仓库与意图] --> B[证据地图]
    B --> C{阅读模式}
    C -->|简约 / 产品| D[定位 + 证明]
    C -->|编辑 / 参考| D
    D --> E[最短上手路径]
    E --> F[事实 · 链接 · 语气验证]
    F --> G[README 成稿]
```

## 立即使用

将 [`SKILL.md`](./SKILL.md) 与 [`references/`](./references/) 放入编码助手的 skill 目录，然后发送一条具体请求：

```text
使用 generate-readme，重写当前项目的中英双语 README。
先给出最短可运行路径；用仓库中的真实输出或图示证明价值；
所有命令、版本和能力都必须能追溯到仓库证据。
```

你会得到一份以项目定位开场、带有可信证明、能引导首次成功操作，并经过事实与读者视角复核的 README。

## 按目标选择入口

| 你想做什么 | 从哪里开始 | 结果 |
|------------|------------|------|
| 快速生成或重写 | [`SKILL.md`](./SKILL.md) | 一条完整的生成工作流 |
| 选择版式与视觉节奏 | [`design-and-structure.md`](./references/design-and-structure.md) | 与项目性格匹配的结构 |
| 判断哪些内容可以写 | [`evidence-and-scan.md`](./references/evidence-and-scan.md) | 已确认 / 可推导 / 未知的证据边界 |
| 检查成稿是否可靠 | [`verification.md`](./references/verification.md) | 事实、链接、层级和语气复核 |

## 它如何做出“智能”判断

- **证据优先**：命令、版本、路由、外部服务和许可证都要能回到清单、配置、源码或维护中的文档。
- **路径优先**：识别主要读者动作；有多个真实入口时，提供清晰的选择表，并突出一条推荐路径。
- **证明优先**：优先放置一个真实输出、截图、图表、完整示例或职责明确的 Mermaid 图，再展开细节。
- **边界清晰**：把可调整参数与不可破坏的核心原则分开，避免把推测写成承诺。
- **渐进展开**：把配置、API、运维和贡献信息放到首次成功之后，必要时链接到专门文档。

## 设计取舍

它借鉴了两个不同方向的成熟做法：创意 skill 常用的居中定位、示例画廊、双入口和参数表；开发工具 README 常用的问题→机制→结果叙事、可复制 Quick Start、架构图、可复现数据和透明局限。这里保留方法，不复制项目内容或装饰。

## 内容边界

不会读取或展示凭据、私有环境文件、日志、数据库转储、依赖目录、构建产物和版本控制内部文件。没有证据的徽章、下载量、兼容性、性能、部署状态、API 行为或许可证信息会被省略或明确标为未知。

## 文件布局

```text
wisdom-readme/
├── SKILL.md
├── references/
│   ├── design-and-structure.md
│   ├── evidence-and-scan.md
│   └── verification.md
├── README.md
├── README.zh-CN.md
├── README.en.md
└── LICENSE
```

根目录是编辑源；`.agents/`、`.claude/`、`.codex/`、`.cursor/` 与 `.trae/` 保存可直接安装的平台副本。

## 许可证

[Apache License 2.0](./LICENSE)
