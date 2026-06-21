# generate-readme

[中文](./README.zh-CN.md) | [English](./README.en.md)

> A README generation skill for AI coding assistants: it creates Chinese, English, or bilingual project documentation from real repository evidence while avoiding private configuration and secrets.

## Overview

`generate-readme` helps users create rigorous and maintainable README documentation. Its goal is not to make a repository sound bigger than it is; its job is to document what can be verified from the files that actually exist.

This skill supports backend, frontend, full-stack, CLI, and library projects. It scans project structure, manifest files, entry points, route or API evidence, existing documentation, and license information before deciding which README sections are appropriate.

## Use Cases

- Create the first `README.md` for a new project
- Turn an existing project into Chinese or English documentation
- Extract installation, run, test, and build instructions for frontend, backend, full-stack, CLI, and library projects
- Document tech stack, project structure, API entry points, and development notes from real code
- Generate bilingual documentation as `README.zh-CN.md` and `README.en.md`
- Produce useful documentation without reading private configuration or credential files

## How To Trigger

After installing this skill in an AI assistant that supports skills, ask for README generation in natural language.

Common prompts:

```text
给这个项目生成 README
生成中文 README
生成英文 README
生成双语项目文档
用 generate-readme 给当前仓库写文档
create a readme for this repository
generate readme language: both
```

The skill metadata exposes this argument hint:

```text
[language: zh|en|both]
```

Argument behavior:

| Argument | Output |
|----------|--------|
| `zh` | Generate a Chinese README, usually targeting `README.md` |
| `en` | Generate an English README, usually targeting `README.md` |
| `both` | Generate `README.zh-CN.md` and `README.en.md` |
| omitted | Infer the language from the user request, existing docs, and project audience |

## Recommended Prompts

For Chinese documentation:

```text
使用 generate-readme，为当前仓库生成中文 README。
请基于真实文件扫描，不要编造功能、部署方式或 API。
```

For English documentation:

```text
Use generate-readme to create an English README for this repository.
Only document facts that can be verified from the codebase.
```

For bilingual documentation:

```text
使用 generate-readme 生成双语文档，language: both。
请分别创建 README.zh-CN.md 和 README.en.md，并保持事实一致。
```

When a README already exists:

```text
使用 generate-readme 检查现有 README，并生成一份 README.generated.md，不要覆盖原文件。
```

## Workflow

The skill works in this order:

1. **Safe project scan**: read only files that help documentation, skipping dependencies, build output, logs, database files, private configuration, and key material.
2. **Existing README check**: if a target README already exists, ask whether to overwrite, create a separate file, or merge content unless overwrite was explicitly requested.
3. **Project type detection**: infer language and project type from files such as `package.json`, `pyproject.toml`, `pom.xml`, `go.mod`, entry points, and directory layout.
4. **Evidence extraction**: collect tech stack, commands, structure, APIs, and notes from manifests, source files, configuration, existing docs, and route definitions.
5. **README generation**: include only sections backed by evidence, and skip empty or placeholder sections.
6. **Quality check**: verify that no sensitive files were read, no architecture was invented, and no private configuration was written into the README.

## Generated Content

The skill chooses sections based on the project instead of forcing a fixed template. Common sections include:

- Project summary
- Features
- Tech stack
- Project structure
- Getting started
- Configuration
- Run, test, and build commands
- API documentation
- Deployment notes
- Development notes
- Security and privacy
- License

If the repository does not include API evidence, deployment configuration, or a license file, the skill does not invent those sections.

## Safety Rules

`generate-readme` explicitly avoids reading, summarizing, or displaying these files:

- `.env`, `.env.*`, `*.env`
- Private Spring configuration such as `application-prod.yml` and `application-local.yml`
- Keys, certificates, and credential files such as `*.pem`, `*.key`, `credentials.*`, and `secrets.*`
- Database, dump, and log files such as `*.db`, `*.sqlite`, `*.sql`, and `*.log`
- Dependencies, caches, and build output such as `node_modules/`, `dist/`, `build/`, and `target/`

When private configuration files are present, the generated README uses a general note instead of listing exact paths or repeating file contents.

## Installation Layout

This repository contains skill copies for multiple assistants.

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

Each platform usually reads the `SKILL.md` under its own directory. If you maintain one source of truth, edit the root `SKILL.md` first and then sync it into the platform-specific directories.

## Codex Interface Metadata

`.codex/skills/generate-readme/agents/openai.yaml` defines how this skill appears in the Codex interface:

```yaml
interface:
  display_name: Generate README
  short_description: Generate evidence-based Chinese or English README files without scanning private config.
  default_prompt: Use Generate README to create concise, bilingual project documentation from the current repository.
```

## Maintenance Notes

- Update the root `SKILL.md` first when changing skill behavior.
- Keep `.agents`, `.claude`, `.codex`, `.cursor`, and `.trae` copies aligned when publishing to multiple assistants.
- When adding rules, describe both what the skill may do and what it must avoid.
- Keep safe scanning conservative; it is better to read less than to pull credentials or production configuration into a README.
- Preserve the core constraints: evidence first, no invented claims, and concise output.

## License

This project is licensed under the [Apache License 2.0](LICENSE).
