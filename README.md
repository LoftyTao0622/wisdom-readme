# generate-readme

> 一个面向 AI 编码助手的 README 生成技能：从真实仓库内容出发，生成中文、英文或双语项目文档，并避免读取或暴露私有配置。

## 概览

`generate-readme` 用来帮助使用者为项目生成严谨、可维护的 README。它的核心目标不是把仓库包装得更好看，而是把仓库里已经存在、可以验证的事实写清楚。

这个技能适用于后端、前端、全栈、CLI 和库项目。它会先扫描项目结构、清单文件、入口文件、路由或 API 证据、现有文档和许可证信息，再决定 README 里应该包含哪些内容。

## 适用场景

- 为新项目生成第一份 `README.md`
- 把已有项目整理成中文或英文文档
- 为前端、后端、全栈、CLI、库项目提炼安装、运行、测试说明
- 根据真实代码提取技术栈、目录结构、API 入口和开发说明
- 生成双语文档：`README.zh-CN.md` 与 `README.en.md`
- 在不读取私有配置和密钥文件的前提下完成文档生成

## 如何触发

在支持 skill 的 AI 助手中，把这个技能安装到对应目录后，直接用自然语言提出 README 生成请求即可。

常见触发方式：

```text
给这个项目生成 README
生成中文 README
生成英文 README
生成双语项目文档
用 generate-readme 给当前仓库写文档
create a readme for this repository
generate readme language: both
```

技能元数据中的参数提示为：

```text
[language: zh|en|both]
```

参数含义：

| 参数 | 输出方式 |
|------|----------|
| `zh` | 生成中文 README，默认目标通常是 `README.md` |
| `en` | 生成英文 README，默认目标通常是 `README.md` |
| `both` | 生成 `README.zh-CN.md` 和 `README.en.md` |
| 未指定 | 根据用户语言、现有文档和项目受众推断 |

## 推荐提示词

中文项目：

```text
使用 generate-readme，为当前仓库生成中文 README。
请基于真实文件扫描，不要编造功能、部署方式或 API。
```

英文项目：

```text
Use generate-readme to create an English README for this repository.
Only document facts that can be verified from the codebase.
```

双语文档：

```text
使用 generate-readme 生成双语文档，language: both。
请分别创建 README.zh-CN.md 和 README.en.md，并保持事实一致。
```

已有 README 时：

```text
使用 generate-readme 检查现有 README，并生成一份 README.generated.md，不要覆盖原文件。
```

## 工作流程

这个技能会按以下顺序工作：

1. **安全扫描项目**：只读取对文档有帮助的文件，跳过依赖、构建产物、日志、数据库文件、私有配置和密钥材料。
2. **检查现有 README**：如果目标 README 已存在，会先询问是覆盖、另存还是合并，除非用户明确要求覆盖。
3. **识别项目类型**：根据 `package.json`、`pyproject.toml`、`pom.xml`、`go.mod`、入口文件和目录结构判断项目语言和类型。
4. **提取可验证信息**：从清单、源码、配置、现有文档和路由定义中提炼技术栈、命令、目录结构、API 和注意事项。
5. **生成 README**：只写有证据支持的章节，跳过空章节和占位内容。
6. **质量检查**：确认没有读取敏感文件，没有编造架构，没有把私有配置写入文档。

## 生成内容

技能会根据项目实际情况选择章节，而不是固定套模板。常见章节包括：

- 项目简介
- 功能特性
- 技术栈
- 项目结构
- 快速开始
- 配置说明
- 运行、测试、构建命令
- API 说明
- 部署说明
- 开发说明
- 安全与隐私
- 许可证

如果仓库没有 API、部署配置或许可证文件，技能不会强行编写这些内容。

## 安全规则

`generate-readme` 明确要求不要读取、总结或展示以下内容：

- `.env`、`.env.*`、`*.env`
- 私有 Spring 配置，例如 `application-prod.yml`、`application-local.yml`
- 密钥、证书和凭据文件，例如 `*.pem`、`*.key`、`credentials.*`、`secrets.*`
- 数据库、转储和日志文件，例如 `*.db`、`*.sqlite`、`*.sql`、`*.log`
- 依赖、缓存和构建产物，例如 `node_modules/`、`dist/`、`build/`、`target/`

如果发现私有配置文件，README 只会写通用说明，不会列出精确路径或复述文件内容。

## 安装位置

这个仓库包含多个平台的技能副本，方便在不同助手中使用。

```text
wisdom-readme/
├── SKILL.md
├── .agents/
│   └── skills/generate-readme/SKILL.md
├── .claude/
│   └── skills/generate-readme/SKILL.md
├── .codex/
│   └── skills/generate-readme/
│       ├── SKILL.md
│       └── agents/openai.yaml
├── .cursor/
│   └── skills/generate-readme/SKILL.md
└── .trae/
    └── skills/generate-readme/SKILL.md
```

不同平台通常会读取各自目录下的 `SKILL.md`。如果你只维护一份主版本，可以先编辑根目录 `SKILL.md`，再同步到对应平台目录。

## Codex 展示配置

`.codex/skills/generate-readme/agents/openai.yaml` 提供了 Codex 界面里的显示信息：

```yaml
interface:
  display_name: Generate README
  short_description: Generate evidence-based Chinese or English README files without scanning private config.
  default_prompt: Use Generate README to create concise, bilingual project documentation from the current repository.
```

## 维护建议

- 修改技能行为时，优先更新根目录 `SKILL.md`。
- 如果面向多个助手发布，保持 `.agents`、`.claude`、`.codex`、`.cursor`、`.trae` 下的说明一致。
- 新增规则时，把“允许做什么”和“禁止做什么”都写清楚。
- 对安全扫描规则要保守，宁可少读文件，也不要把凭据或生产配置带进 README。
- 如果调整输出风格，保留“基于证据、不编造、不过度冗长”的核心约束。

## 许可证

我还没有在仓库中发现许可证文件；在补充 `LICENSE` 之前，这个技能默认只按仓库当前权限使用。
