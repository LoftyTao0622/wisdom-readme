---
name: generate-readme
description: Generate rigorous, evidence-based README documentation for any software project. Use this skill when the user asks to "create a readme", "generate readme", "write documentation", "生成readme", "写文档", "生成项目文档", or requests README files in any language.
version: 2.0.0
argument-hint: "[language: <locale>]"
user-invocable: true
allowed-tools:
  - Read
  - Glob
  - Grep
  - Bash
  - Write
---

# README Generator

Generate polished, reader-centric README documentation from actual repository contents.

## README Quality Rubric

Before generating, internalize these six criteria. A successful README must satisfy ALL of them. After writing, verify each one (see Verification Pass).

1. **Reader-first journey** — The README answers questions a new reader asks, in order:
   "What is this?" → "Should I use it?" → "How do I start?" → "Where do I go next?"
   The reader is someone who found this repo and wants to know what it does and how to use it in under 5 minutes.

2. **Evidence-backed** — Every feature, command, endpoint, version number, and architectural claim is traceable to a file in the repository. If the evidence is ambiguous, omit the claim.

3. **Actionable** — Every command shown is exact and verifiable from build files or scripts. Every configuration key documents its purpose. The reader can copy-paste and run.

4. **Scannable** — Skimming headers alone tells the story. Code blocks are minimal (≤10 lines). Technical details have a home (API table, config reference) — they are not scattered through narrative paragraphs.

5. **WHAT not HOW** — The README describes what the project does and how to use it. Internal implementation details (class hierarchy, algorithm choices, code structure walkthrough) belong in developer docs or CONTRIBUTING.md — not in the README.

6. **Maintainer voice** — Reads as if the project maintainer wrote it for a new team member. No AI self-reference ("I scanned", "the model found"), no generic advice ("it is recommended that"), no filler.

## Step 1: Understand The Project First

Before scanning files, establish what this project IS and who it's FOR. Read in priority order:

1. Any existing README (`README.md`, `README.*.md`, `docs/`)
2. Project description field in manifests (`package.json` description, `pyproject.toml` description, `pom.xml` description, `Cargo.toml` description, `mix.exs` description, `*.gemspec` summary)
3. Top-level directory layout
4. Entry-point files (CLI main, server startup, app bootstrap)

From these, answer: **what problem does this project solve, and for whom?** This answer shapes every section that follows. Do not proceed to scanning until you can state it in one sentence.

## Step 2: Choose The Right Structure

Pick the structure that serves THIS project's readers. The sections below are patterns, not mandates — adapt to what the project actually needs.

### Pattern A: Library / SDK

For packages consumed by other code.

```
# Name
One-line: what it does, what problem it solves.

## Installation
## Quick Start (minimal working example: install → import → use)
## Usage (organized by task, not by class/method)
## API Reference (link or compact table)
## Configuration (if any)
## License
```

### Pattern B: Application / Service

For deployable services and applications.

```
# Name
One-line: what the service does, its role.

## Architecture Overview (if multi-component — keep to 5-9 nodes)
## Prerequisites
## Setup & Installation
## Configuration Reference
## Running
## API (if applicable — compact table: Method | Path | Purpose | Source)
## Operations / Deployment
## License
```

### Pattern C: CLI Tool

For command-line utilities.

```
# Name
One-line: what the tool does.

## Installation
## Quick Examples (3-5 most common invocations with their output intent)
## Command Reference
## Configuration
## Development
## License
```

### Pattern D: Full-Stack / Monorepo

For projects with both frontend and backend.

```
# Name
One-line: what the project does.

## Architecture Overview
## Backend
   ### Prerequisites, Setup, Configuration, Running
## Frontend
   ### Prerequisites, Setup, Configuration, Running
## Shared / Development Workflow
## Deployment
## License
```

### Structure Principles

- Start with what the reader needs to know FIRST. What is it → how to get it running. Everything else supports these two.
- A section exists because it answers a real question, not because a template has it. Omit empty sections without comment.
- Complex commercial projects need more detail — that's expected. The README should be as long as the project requires and no longer. Do not pad; do not truncate to hit an arbitrary line count.
- If the project already has a README with a well-organized structure and visual identity (badges, centered headers, Mermaid diagrams), preserve and update it in place. Do not flatten existing polish into a generic template.

## Step 3: Safe Project Scan

### Excluded Paths

Never read, grep, or display content from:

- VCS: `.git/`, `.svn/`, `.hg/`
- Dependencies: `node_modules/`, `vendor/`, `.venv/`, `venv/`, `env/`, `__pycache__/`
- Build output: `dist/`, `build/`, `.next/`, `.nuxt/`, `out/`, `.svelte-kit/`, `coverage/`, `target/`, `bin/`, `obj/`, `.gradle/`, `classes/`
- Cache: `.npm/`, `.pnpm-store/`, `.yarn/`
- Logs & dumps: `*.log`, `logs/`, `dump/`, `*.dump`, `*.sql`, `*.sqlite`, `*.db`
- Private config: `.env`, `.env.*`, `*.env`, `application-local.*`, `application-prod.*`, `bootstrap-prod.*`, `settings.local.*`, `local_settings.*`
- Credentials: `*.pem`, `*.key`, `*.p12`, `*.pfx`, `id_rsa*`, `id_ed25519*`, `credentials.*`, `secrets.*`, `secret.*`, `service-account*.json`, `kubeconfig`

Safe example files MAY be read: `.env.example`, `.env.sample`, `config.example.*`, `application-example.*`

When private files exist, do not call out their exact paths in the README. Use a general note or omit entirely.

### Scan Order

1. **Existing docs** — `README.md`, `README.*.md`, `docs/`, `CHANGELOG.md`, `CONTRIBUTING.md`, `LICENSE`
2. **Manifests** — detect language, framework, dependencies, versions
3. **Entry points** — main source, server startup, CLI entry, route definitions
4. **Configuration** — example config, env templates, config structs/models
5. **Project tree** — source layout, test layout, deployment configs

### Project Type Detection

Use the following signals to identify the implementation language(s). When multiple languages coexist, identify each one's role (e.g., "Python backend + TypeScript frontend") — do not force a single label.

| Ecosystem | Key Signals |
|-----------|-------------|
| Node.js / TypeScript | `package.json`, `tsconfig.json`, `vite.config.*`, `next.config.*`, `nuxt.config.*` |
| Python | `pyproject.toml`, `requirements*.txt`, `setup.py`, `setup.cfg`, `Pipfile`, `uv.lock`, `poetry.lock` |
| Java / Kotlin | `pom.xml`, `build.gradle`, `build.gradle.kts`, `settings.gradle` |
| Go | `go.mod`, `cmd/`, `main.go`, `internal/` |
| Rust | `Cargo.toml`, `src/main.rs`, `src/lib.rs` |
| C# / .NET | `*.csproj`, `*.sln`, `*.fsproj`, `Program.cs` |
| Ruby | `Gemfile`, `*.gemspec`, `Rakefile` |
| PHP | `composer.json`, `index.php`, `artisan` |
| Elixir | `mix.exs`, `lib/`, `config/` |
| C / C++ | `CMakeLists.txt`, `Makefile`, `configure.ac`, `meson.build` |
| Swift | `Package.swift`, `*.xcodeproj`, `*.xcworkspace` |
| Dart / Flutter | `pubspec.yaml`, `lib/main.dart` |
| Zig | `build.zig`, `src/main.zig` |
| Shell | `*.sh` with project-scale structure, `Makefile`-only projects |

README handling rules by ecosystem:

- **Node.js/TS**: Detect package manager from lockfile (`pnpm-lock.yaml` → pnpm, `yarn.lock` → yarn, `package-lock.json` → npm, `bun.lockb` → bun). Extract real scripts from `package.json`. Separate frontend/backend when both exist.
- **Python**: Detect tooling (`uv.lock` → uv, `poetry.lock` → Poetry, `Pipfile` → Pipenv, `requirements*.txt` → pip). For web frameworks, document the actual run command found in code or scripts.
- **Java/Kotlin**: Detect Maven vs Gradle. Identify framework from dependencies (Spring Boot, Quarkus, Micronaut). Do not read private Spring profile files.
- **Go**: Use module path from `go.mod`. For CLI tools, include command examples from flag definitions. For services, document routes from explicit router registrations.
- **Rust**: Detect binary vs library from `Cargo.toml`. Use `cargo` commands. For CLI, extract help text or arg definitions.
- **C#/.NET**: Use `dotnet` commands. Identify project type (web, console, library) from `.csproj`.
- **Ruby**: Detect gem vs Rails app. Use `bundle`/`gem` commands accordingly.
- **PHP**: Detect Composer packages vs Laravel/Symfony apps. Use appropriate artisan/console commands.
- **Elixir**: Detect Mix project type. Use `mix` commands. Identify Phoenix if present.
- **Dart/Flutter**: Detect pure Dart vs Flutter. Use `dart`/`flutter` commands accordingly.

## Step 4: Content Generation Rules

### Overview

2-4 sentences answering: **What does this project do? Who is it for? What problem does it solve?** Ground in the project description from manifests, existing docs, or entry-point comments.

Do NOT describe the tech stack here, do NOT list features, do NOT say "built with X and Y."

### Features

- List user-visible capabilities only. Not implementation details.
- Each feature: one line describing what it does, not how.
- BAD: "Uses Redis for caching" — GOOD: "Fast responses with automatic caching"
- BAD: "Implemented with Spring Security" — GOOD: "Role-based access control for admin and user accounts"
- Group related features. List only what the project actually has — do not pad.

### Tech Stack

A categorized reference table, not narrative prose. Include only categories with evidence:

| Category | Technology | Version | Purpose |
|----------|-----------|---------|---------|
| Runtime | Node.js | 22 | Server runtime |

Keep to one row per distinct technology. Group related items under category headers.

### Project Structure

Compact directory tree:
- Max depth 3 (deeper only if showing a critical subdirectory)
- Max 40 lines
- Show: source, config, tests, docs, deployment files
- Omit: build output, dependencies, generated code, private config

### Getting Started

Every command shown must be verifiable from the project's build files, scripts, or Makefile.

- **Prerequisites**: runtime versions, required external services (database, cache, etc.) — only what the project actually needs.
- **Installation**: exact commands from clone to dependencies installed. One path, not every possible variant.
- **Configuration**: what env vars or config files must be set, what each key means for running the project. Derive from example config files.
- **Run**: the exact command(s) to start the project.
- **Test**: the exact command to run tests.

### API

Only include if route definitions or OpenAPI files exist.

Use a compact table:

| Method | Path | Purpose | Source |
|--------|------|---------|--------|
| GET | `/api/users` | List users | `src/routes/users.ts:42` |

Rules:
- Extract method and path only when both are explicit in source.
- Do not infer request/response schemas, auth, rate limits, or error codes without evidence.
- If >15 endpoints, show representative groups and link to the OpenAPI file or route directory.
- If route construction is dynamic, note it briefly: "Routes are assembled at runtime; see `src/routes/` for definitions."

### Architecture Diagram

Include a Mermaid diagram only when the repository clearly shows multiple interacting components.

- Max 7-9 nodes.
- Label nodes with component names (e.g., "API Server", "Web Frontend"), not technology names (e.g., "Express.js", "React").
- Do not draw external services (databases, queues, clouds) unless explicitly configured in the project.
- If architecture is simple or evidence is weak, omit the diagram.

### Security, Privacy, and License

Use maintainer-first language. No generic AI advice.

Security & Privacy (when sensitive data is involved):

```markdown
## 安全与隐私

项目默认配置只保留运行所需的配置结构。生产环境中的密钥、密码和凭据应通过环境变量或私有配置注入，不建议写入仓库。

系统处理患者主诉、检查资料、诊断结论等医疗数据。演示、测试和截图请优先使用脱敏数据。
```

```markdown
## Security And Privacy

Default configuration documents the structure needed to run the project. Production keys, passwords, and credentials should be injected through environment variables or private configuration — not committed.

This system handles medical data. Use de-identified data for demos, tests, and screenshots.
```

License:
- If a license file exists, name it accurately and link to it.
- If no license file exists, state it factually without legal advice or pressure:

```markdown
## License

当前仓库未提供独立的 `LICENSE` 文件。对外分发或开源前，请补充明确的许可证文本。
```

```markdown
## License

This repository does not currently include a standalone `LICENSE` file. Add an explicit license before public distribution or open-source release.
```

## Step 5: Content Quality Rules

### MUST Include
- What the project does and who it's for (first 5 lines)
- How to install, configure, run, and test (exact, verified commands)
- What external dependencies or services are needed
- Where to find more (docs, API reference, contributing guide, website)
- License status (factual only)

### MUST Exclude
- Code blocks longer than 10 lines — link to source files instead
- Log output, error messages, stack traces, terminal dumps
- Implementation details: class hierarchy, algorithm choices, internal architecture walkthrough
- Generic advice: "it is recommended to use proper error handling", "you should follow best practices"
- AI self-reference: "I scanned", "I found", "according to the repository", "the model detected"
- Filler: "This section will be updated", "TODO", "TBD", "coming soon"
- Duplicate content across sections — say it once, in the right place

### Tone Rules
- **Direct, not hedged**: "Install dependencies:" not "You can install dependencies by running:"
- **Factual, not speculative**: "Supports PostgreSQL" not "Should work with most databases"
- **Maintainer, not AI**: Write as the person who built the project. Never use first-person to describe what the model did.
- **Consistent**: Same voice in every section. If the Overview is informal, the API reference shouldn't sound like a legal document.

## Step 6: Handling Existing READMEs

If a target file already exists:
1. Stop and tell the user which file exists.
2. Ask: overwrite, create a separate file, or merge.
3. Proceed only after the user chooses (unless they already gave explicit overwrite permission).

Target file rules:
- Language specified by user → generate in that language to `README.md` (or `README.<locale>.md`).
- No language specified → infer from existing docs or user's message language.
- Bilingual/multilingual → separate files per language. Optionally a short `README.md` index linking to them:

```markdown
# Project Name

- [中文文档](./README.zh-CN.md)
- [English Documentation](./README.en.md)
```

Do NOT mix languages within the same file except for code, commands, package names, and standard technical identifiers.

## Step 7: Bilingual & Multilingual Generation

- Create separate files per language.
- Keep structure and facts equivalent across all versions.
- Localize naturally — do not machine-translate. Section names, explanations, and notes should sound native in each language.
- Code, commands, and technical identifiers remain in their original language.
- Support any human language the user requests. If unsure, ask.

## Step 8: MANDATORY Verification Pass

After writing the README, perform a second pass. This is NOT optional. Check each item against the generated output, and fix any failures before reporting done.

### A. Factual Accuracy
For each claim in the README, trace it to a source file:

- [ ] Every command (`npm run dev`, `go build`, `cargo test`, etc.) exists in build files, scripts, or Makefile.
- [ ] Every API endpoint (method + path) was found in source code or an OpenAPI file.
- [ ] Every version number comes from a manifest or lockfile.
- [ ] Every external service mentioned (database, cache, queue, third-party API) has corresponding dependency or config evidence.
- [ ] Architecture node descriptions match source directories or documented modules.
- [ ] License name matches the actual `LICENSE` file. If no license file, the README states so without inventing one.

### B. Content Integrity
Inspect the generated README line by line:

- [ ] First 5 lines tell the reader what the project does and who it's for.
- [ ] No code block exceeds 10 lines.
- [ ] No log output, error messages, stack traces, or terminal dumps appear.
- [ ] No AI self-reference anywhere (`grep` for: "I scanned", "I found", "according to", "the model", "the agent", "the repository shows").
- [ ] No filler or placeholder content (`grep` for: "TODO", "TBD", "coming soon", "will be added", "placeholder").
- [ ] No implementation-detail narrative: class hierarchy, algorithm walkthrough, "the code is organized as follows"-style paragraphs.

### C. Structure Quality
Verify the reader's journey:

- [ ] Every section answers a real reader question. No section exists solely because a template includes it.
- [ ] Tech stack is a reference table, not narrative prose.
- [ ] The README would let a new developer clone, configure, and run the project without asking questions.
- [ ] Existing visual style (badges, centered headers, Mermaid diagrams) is preserved unless explicitly asked to change.

### D. Tone
Read the entire README as if you're a new team member:

- [ ] Consistent voice — same person appears to have written every section.
- [ ] No hedging ("should work", "may need", "it is recommended", "please note that").
- [ ] No generic advice divorced from this specific project.

If any check fails, fix it. Do not report the README as complete until all checks pass.
