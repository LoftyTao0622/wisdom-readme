<div align="center">

<sub><strong>AI 编码助手技能&nbsp;&nbsp;·&nbsp;&nbsp;文档生成系统</strong></sub>

# generate-readme

从真实仓库证据出发，生成严谨、可执行、以读者为中心的 README。

<a href="./README.zh-CN.md"><img src="https://img.shields.io/badge/中文-README-C2415A?style=flat-square&labelColor=F6E7EA" alt="中文 README"></a>
<a href="./README.en.md"><img src="https://img.shields.io/badge/English-README-2F6F68?style=flat-square&labelColor=E3F0EE" alt="English README"></a>
<img src="https://img.shields.io/badge/支持_14_种生态-6B5B95?style=flat-square&labelColor=EEEAF4" alt="支持 14 种编程语言生态">
<img src="https://img.shields.io/badge/证据驱动文档-D28A3D?style=flat-square&labelColor=F7EEDD" alt="证据驱动文档">

<p>
  <a href="./README.zh-CN.md">中文</a>
  <span> · </span>
  <a href="./README.en.md">English</a>
</p>

</div>

## 能做什么

`generate-readme` 帮助使用者从零生成或改进项目的 README 文档。它不是把仓库包装得更好看，而是把仓库里可验证的事实写得清晰、可操作。

**核心约束：**

- **读者优先**：按新读者的阅读路径组织内容 — "这是什么 → 我能用它吗 → 怎么开始 → 去哪了解更多"
- **证据驱动**：每个功能、命令、API 端点、版本号都有源文件可追溯；证据模糊的内容直接省略
- **可执行**：每条命令都能从构建文件或脚本中验证；读者可以复制粘贴运行
- **WHAT 不是 HOW**：README 描述项目做什么、怎么用；实现细节留给开发者文档
- **维护者语气**：写得像项目维护者在给新同事讲解，不是 AI 在报告扫描结果

**冲突处理：**

- 证据优先于排版：无法从仓库确认的徽章、版本、命令、端点和架构声明不写入 README
- 读者定位优先于元数据：标题附近的徽章和语言导航不算项目介绍，开头内容块必须明确项目是什么、面向谁
- 保留既有视觉风格：更新已有 README 时保留有效的徽章、居中标题、导航和 Mermaid 图，不强行套用模板
- 按用户要求覆盖默认行为；项目没有测试、配置或部署路径时，不虚构对应章节和命令

**支持的能力：**

- 自动检测 14 种编程语言生态（Node/TS、Python、Java/Kotlin、Go、Rust、C#/.NET、Ruby、PHP、Elixir、C/C++、Swift、Dart/Flutter、Zig、Shell）
- 按项目类型自适应结构：库/SDK、应用服务、CLI 工具、全栈/单体仓库
- 从源码中提取可验证的 API 端点、目录结构、配置项
- 区分徽章、项目介绍、功能列表、技术栈表和架构图，避免技术标签与开头定位说明互相冲突
- 支持混合型项目和 monorepo，优先说明读者最需要执行的主路径
- 更新已有 README 时根据用户意图选择合并或重写，并保留可验证的项目专属信息
- 生成任意人类语言的 README（中文、英文、日文等）
- 双语文档保持结构和事实对齐
- 在不读取私有配置、密钥、日志和构建产物的前提下完成所有工作

## 快速开始

### 安装

把本仓库的 `SKILL.md` 复制到对应助手的技能目录，或直接 clone 到技能目录下：

```text
# Claude Code
.claude/skills/generate-readme/SKILL.md

# Codex
.codex/skills/generate-readme/SKILL.md

# Cursor
.cursor/skills/generate-readme/SKILL.md

# Trae
.trae/skills/generate-readme/SKILL.md
```

### 触发

安装后直接用自然语言提出请求：

```text
给这个项目生成 README
create a readme for this repository
generate readme language: both
日本語のREADMEを生成して
```

### 参数

```text
[language: <locale>]
```

| 参数 | 行为 |
|------|------|
| `zh` | 生成中文 README |
| `en` | 生成英文 README |
| `<locale>` | 生成任意语言的 README（如 `ja`、`fr`、`ko`） |
| `both` | 分别生成 `README.zh-CN.md` 和 `README.en.md` |
| 未指定 | 根据用户语言、已有文档和项目受众推断 |

### 推荐提示词

```text
使用 generate-readme，为当前仓库生成中文 README。
请基于真实文件扫描，不要编造功能、部署方式或 API。
```

```text
Use generate-readme to create an English README for this repository.
Only document facts that can be verified from the codebase.
```

## 工作流程

1. **理解项目**：先读已有 README、项目描述字段、目录布局，形成有证据支持的项目定位说明
2. **选择结构**：根据主要读者动作和项目类型（库/应用/CLI/全栈）选择最适合的章节组织
3. **安全扫描**：读取清单、入口文件、路由定义、配置示例，跳过依赖、构建产物、日志和凭据
4. **生成内容**：先确定开头内容块，再按读者路径编写；每项声明都有源文件支持
5. **交叉验证**：核对徽章、正文、技术栈、架构图和多语言版本之间是否一致
6. **强制复查**：确认命令可执行、端点真实存在、无 AI 自述或占位内容、章节非空且语气一致

## 安全规则

以下路径永远不会被读取或展示：

- 凭据和密钥：`.env`、`*.pem`、`*.key`、`credentials.*`、`secrets.*`、`kubeconfig`
- 私有配置：`application-prod.yml`、`application-local.yml`、`settings.local.py`
- 依赖和构建产物：`node_modules/`、`dist/`、`build/`、`target/`、`.next/`
- 日志和数据库：`*.log`、`*.sqlite`、`*.db`、`*.sql`

发现私有文件时不会在 README 中暴露路径。

## 项目布局

```text
wisdom-readme/
├── SKILL.md              ← 主版本（编辑入口）
├── LICENSE
├── README.md             ← 短索引
├── README.zh-CN.md
├── README.en.md
├── .agents/skills/generate-readme/
├── .claude/skills/generate-readme/
├── .codex/skills/generate-readme/
├── .cursor/skills/generate-readme/
└── .trae/skills/generate-readme/
```

各平台目录下的 `SKILL.md` 与根目录主版本保持同步。

## 维护

- 修改技能行为时优先编辑根目录 `SKILL.md`，再同步到各平台目录
- 根目录 `SKILL.md` 是唯一来源；同步后应检查六份文件内容一致
- 安全扫描规则宁可保守：少读文件比把凭据写进 README 好
- 保留核心约束：证据优先、不编造、以读者为中心，并让徽章和项目介绍各司其职

## 许可证

[Apache License 2.0](LICENSE)
