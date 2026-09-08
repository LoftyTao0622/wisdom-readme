<div align="center">

<sub>面向 AI 编码助手的 README 写作技能</sub>

# generate-readme

从真实仓库证据出发，把项目写得准确、自然，也让第一次阅读变得轻松。

[中文](./README.zh-CN.md) · [English](./README.en.md)

</div>

## 为什么需要它

好的 README 不是目录树、技术栈和徽章的集合。它要先帮助读者判断项目是否适合自己，再用一个可信的例子建立理解，最后给出一条不会卡住的上手路径。

`generate-readme` 把这件事拆成两类判断：仓库证据决定内容边界，项目性格决定叙事与版式。最终文档读起来像维护者写给新用户的说明，而不是一次代码扫描报告。

## 快速使用

将 [`SKILL.md`](./SKILL.md) 与 [`references/`](./references/) 一起复制到编码助手的 skill 目录：

```text
.codex/skills/generate-readme/
├── SKILL.md
└── references/
```

随后直接提出任务：

```text
使用 generate-readme，重写当前项目的中文 README。
先给出最短可运行路径，保留已有品牌元素，避免无法验证的描述。
```

也可以要求英文、双语或指定地区语言。多语言版本会分别写入文件，事实与命令保持一致，措辞按语言习惯自然重写。

## 它怎样做判断

| 阶段 | 关键问题 | 产出 |
|------|----------|------|
| 定位 | 这是什么，服务谁，带来什么结果？ | 一句话项目定位 |
| 取证 | 命令、版本、能力和架构能否追溯？ | 临时证据表 |
| 设计 | 哪种阅读节奏符合项目本身？ | 结构与视觉模式 |
| 写作 | 怎样让读者完成第一次成功操作？ | 连贯的主路径 |
| 验证 | 技术事实、链接、语气和版式是否成立？ | 修正后的 README |

证据分为“已确认、可推导、未知”三档。源码、清单、配置示例和维护中的项目文档可以支持直接陈述；命名惯例或不完整实现不会被包装成确定事实。

## 四种阅读模式

这个 skill 不再把居中标题和一排徽章当成所有项目的默认答案。它会根据仓库内容选择或组合以下模式：

- **简约型**适合库、基础设施和源码仓库。重点是定位、必要链接与最短入口。
- **产品型**适合应用和开发工具。用真实界面、输出或可复现结果建立信任。
- **编辑型**适合创意工具、精选集合和教育项目。通过标题、段落节奏与留白形成性格。
- **参考型**适合 API、SDK 和多入口 CLI。先帮助读者选择路径，再展开精确用法。

结构通常沿着“定位 → 证明 → 行动 → 深入”展开，但不会为了套模板制造空章节。设计参考吸收了 [Playwright](https://github.com/microsoft/playwright/blob/main/README.md)、[uv](https://github.com/astral-sh/uv/blob/main/README.md)、[FastAPI](https://github.com/fastapi/fastapi/blob/master/README.md)、[Rust](https://github.com/rust-lang/rust/blob/main/README.md) 与 [shadcn/ui](https://github.com/shadcn-ui/ui/blob/main/README.md) 的成熟做法。

## 内容边界

skill 会验证安装、运行、测试、配置、API、外部服务和许可证信息。它不会读取或展示私有环境文件、凭据、日志、数据库转储、依赖目录、构建产物与版本控制内部文件。

以下内容只在确有帮助时出现：

- 徽章用于回答版本、兼容性、构建状态或许可证等真实问题；
- 截图、动图与基准图用于证明主要价值；
- Mermaid 用于解释难以通过短段落说明的组件关系；
- 技术栈只保留会影响安装、集成、运行或贡献的技术。

## 项目结构

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

## 维护

修改行为时先更新根目录的 `SKILL.md` 或相应 reference，再同步各平台副本。使用 skill-creator 提供的验证脚本检查 frontmatter、命名与未完成占位符；内容质量仍需通过真实项目试写和人工阅读判断。

## 许可证

[Apache License 2.0](./LICENSE)
