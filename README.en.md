# generate-readme

[中文](./README.zh-CN.md) | [English](./README.en.md)

> A README generation skill for AI coding assistants — produces rigorous, reader-centric project documentation from real repository evidence.

## What It Does

`generate-readme` helps you create or improve README documentation from scratch. It doesn't polish the repository — it documents what can be verified from the files that exist.

**Core constraints:**

- **Reader-first** — organized by the reader's journey: "What is this → Should I use it → How do I start → Where next"
- **Evidence-backed** — every feature, command, endpoint, and version traces to a source file; ambiguous claims are omitted
- **Actionable** — every command is verified from build files or scripts; the reader can copy, paste, and run
- **WHAT not HOW** — describes what the project does and how to use it; implementation details belong in developer docs
- **Maintainer voice** — reads like a project maintainer explaining things to a new team member, not an AI reporting scan results

**Capabilities:**

- Auto-detects 14 programming language ecosystems (Node/TS, Python, Java/Kotlin, Go, Rust, C#/.NET, Ruby, PHP, Elixir, C/C++, Swift, Dart/Flutter, Zig, Shell)
- Adapts structure by project type: Library/SDK, Application/Service, CLI Tool, Full-stack/Monorepo
- Extracts verifiable API endpoints, directory trees, and configuration keys from source code
- Generates documentation in any human language (Chinese, English, Japanese, etc.)
- Bilingual output with equivalent structure and facts across versions
- All done without reading private config, credentials, logs, or build artifacts

## Quick Start

### Install

Copy `SKILL.md` into your assistant's skills directory, or clone this repo directly into it:

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

### Trigger

After installation, ask in natural language:

```text
create a readme for this repository
给这个项目生成 README
generate readme language: both
日本語のREADMEを生成して
```

### Argument

```text
[language: <locale>]
```

| Argument | Behavior |
|----------|----------|
| `zh` | Generate a Chinese README |
| `en` | Generate an English README |
| `<locale>` | Generate in any language (e.g., `ja`, `fr`, `ko`) |
| `both` | Generate `README.zh-CN.md` and `README.en.md` |
| omitted | Inferred from user request, existing docs, and project audience |

### Recommended Prompts

```text
Use generate-readme to create an English README for this repository.
Only document facts that can be verified from the codebase.
```

```text
使用 generate-readme，为当前仓库生成中文 README。
请基于真实文件扫描，不要编造功能、部署方式或 API。
```

## Workflow

1. **Understand the project** — read existing docs, project description fields, and directory layout to determine what the project does and who it's for
2. **Choose the structure** — pick the right section layout based on project type (library/app/CLI/full-stack)
3. **Safe scan** — read manifests, entry points, route definitions, and example configs; skip dependencies, build output, logs, and credentials
4. **Generate content** — write each section with source-file evidence for every claim
5. **Mandatory verification** — independent second pass: are commands executable, do endpoints exist in source, is there any AI self-reference or placeholder, is the tone consistent

## Safety Rules

These paths are never read or displayed:

- Credentials and keys: `.env`, `*.pem`, `*.key`, `credentials.*`, `secrets.*`, `kubeconfig`
- Private config: `application-prod.yml`, `application-local.yml`, `settings.local.py`
- Dependencies and build output: `node_modules/`, `dist/`, `build/`, `target/`, `.next/`
- Logs and databases: `*.log`, `*.sqlite`, `*.db`, `*.sql`

When private files are present, paths are never exposed in the output.

## Project Layout

```text
wisdom-readme/
├── SKILL.md              ← source of truth (edit here)
├── LICENSE
├── README.md             ← short index
├── README.zh-CN.md
├── README.en.md
├── .agents/skills/generate-readme/
├── .claude/skills/generate-readme/
├── .codex/skills/generate-readme/
├── .cursor/skills/generate-readme/
└── .trae/skills/generate-readme/
```

Platform-specific `SKILL.md` copies are kept in sync with the root version.

## Maintenance

- Edit the root `SKILL.md` first when changing behavior, then sync to platform directories
- Err on the side of conservative scanning — reading fewer files is better than exposing credentials
- Preserve the core constraints: evidence first, no invention, reader-centric output

## License

[Apache License 2.0](LICENSE)
