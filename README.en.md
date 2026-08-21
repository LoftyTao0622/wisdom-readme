<div align="center">

<sub><strong>AI CODING ASSISTANT SKILL&nbsp;&nbsp;·&nbsp;&nbsp;DOCUMENTATION SYSTEM</strong></sub>

# generate-readme

Evidence-backed, actionable README documentation for real software projects.

<a href="./README.zh-CN.md"><img src="https://img.shields.io/badge/中文-README-C2415A?style=flat-square&labelColor=F6E7EA" alt="中文 README"></a>
<a href="./README.en.md"><img src="https://img.shields.io/badge/English-README-2F6F68?style=flat-square&labelColor=E3F0EE" alt="English README"></a>
<img src="https://img.shields.io/badge/14_ecosystems-supported-6B5B95?style=flat-square&labelColor=EEEAF4" alt="14 ecosystems supported">
<img src="https://img.shields.io/badge/evidence--backed-documentation-D28A3D?style=flat-square&labelColor=F7EEDD" alt="Evidence-backed documentation">

<p>
  <a href="./README.zh-CN.md">中文</a>
  <span> · </span>
  <a href="./README.en.md">English</a>
</p>

</div>

## What It Does

`generate-readme` helps you create or improve README documentation from scratch. It doesn't polish the repository — it documents what can be verified from the files that exist.

**Core constraints:**

- **Reader-first** — organized by the reader's journey: "What is this → Should I use it → How do I start → Where next"
- **Evidence-backed** — every feature, command, endpoint, and version traces to a source file; ambiguous claims are omitted
- **Actionable** — every command is verified from build files or scripts; the reader can copy, paste, and run
- **WHAT not HOW** — describes what the project does and how to use it; implementation details belong in developer docs
- **Maintainer voice** — reads like a project maintainer explaining things to a new team member, not an AI reporting scan results

**Conflict handling:**

- Evidence beats presentation: omit badges, versions, commands, endpoints, and architecture claims that cannot be verified from the repository
- Reader orientation beats metadata: badges and language navigation do not count as the project introduction; the opening content block must say what the project is and who it serves
- Preserve useful visual identity: keep valid badges, centered headers, navigation, and Mermaid diagrams when updating an existing README instead of forcing a new template
- Follow explicit user instructions; do not invent configuration, testing, or deployment sections when the project has no verified path for them

**Capabilities:**

- Auto-detects 14 programming language ecosystems (Node/TS, Python, Java/Kotlin, Go, Rust, C#/.NET, Ruby, PHP, Elixir, C/C++, Swift, Dart/Flutter, Zig, Shell)
- Adapts structure by project type: Library/SDK, Application/Service, CLI Tool, Full-stack/Monorepo
- Extracts verifiable API endpoints, directory trees, and configuration keys from source code
- Separates badges, positioning statements, feature lists, tech-stack tables, and architecture diagrams so they do not contradict one another
- Handles mixed projects and monorepos by prioritizing the primary reader action and documenting a clear top-level path
- Updates existing READMEs by inferring whether the user wants a merge or rewrite, while preserving verifiable project-specific details
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

1. **Understand the project** — read existing docs, project description fields, and directory layout to form an evidence-backed positioning statement
2. **Choose the structure** — pick the right section layout based on the primary reader action and project type (library/app/CLI/full-stack)
3. **Safe scan** — read manifests, entry points, route definitions, and example configs; skip dependencies, build output, logs, and credentials
4. **Generate content** — establish the opening content block first, then write each section with source-file evidence for every claim
5. **Cross-check** — reconcile badges, prose, tech-stack tables, architecture diagrams, and multilingual files
6. **Mandatory verification** — independent second pass: are commands executable, do endpoints exist in source, are there AI references or placeholders, and are all sections useful and consistent

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
- Treat the root `SKILL.md` as the single source of truth and verify all six copies after synchronization
- Err on the side of conservative scanning — reading fewer files is better than exposing credentials
- Preserve the core constraints: evidence first, no invention, reader-centric output, and clear separation between badges and project positioning

## License

[Apache License 2.0](LICENSE)
