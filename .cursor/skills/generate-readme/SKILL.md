---
name: generate-readme
description: Generate rigorous, evidence-based README documentation for backend, frontend, full-stack, CLI, and library projects. Use this skill when the user asks to "create a readme", "generate readme", "write documentation", "生成readme", "写文档", "生成项目文档", or requests Chinese/English README files.
version: 1.0.0
---

# README Generator

Generate polished README documentation from the actual repository contents. Be strict about evidence: document what is present, skip what is unknown, and never invent architecture, deployment topology, API behavior, security posture, roadmap, or license terms.

## Core Principles

1. **Evidence first**: every feature, command, API endpoint, dependency, and architectural statement must be traceable to files in the repository.
2. **No secret exposure**: never read, summarize, quote, or list sensitive configuration files or credential-like values.
3. **No overwrite without consent**: if a target README file already exists, ask before overwriting unless the user explicitly requested overwrite.
4. **Language-aware output**: detect the project language first, then choose README sections, commands, and terminology that fit that ecosystem.
5. **Short enough to use**: prefer a focused README over a catalog of every file. Keep generated content concise, attractive, and skimmable.
6. **Human maintainer voice**: security, privacy, and license notes should read like a maintainer's first-person project note, not generic AI advice.

## Step 1: Safe Project Scan

Scan only files that are useful for documentation. Run discovery commands with explicit excludes.

### Must Exclude From Scanning

Do **not** read, grep, summarize, or display content from these files or directories:

- `.git/`, `.svn/`, `.hg/`
- `node_modules/`, `vendor/`, `.venv/`, `venv/`, `env/`, `__pycache__/`
- Frontend build output: `dist/`, `build/`, `.next/`, `.nuxt/`, `out/`, `.svelte-kit/`, `coverage/`
- Backend build output: `target/`, `bin/`, `obj/`, `.gradle/`, `build/`, `classes/`, `generated-sources/`
- JavaScript package caches: `.npm/`, `.pnpm-store/`, `.yarn/`
- Logs and dumps: `*.log`, `logs/`, `dump/`, `dumps/`, `*.dump`, `*.sql`, `*.sqlite`, `*.db`
- Private environment/config files: `.env`, `.env.*`, `*.env`, `application-local.yml`, `application-local.yaml`, `application-prod.yml`, `application-prod.yaml`, `bootstrap-prod.yml`, `bootstrap-prod.yaml`, `settings.local.py`, `local_settings.py`
- Credential/key material: `*.pem`, `*.key`, `*.p12`, `*.pfx`, `id_rsa*`, `id_ed25519*`, `credentials.*`, `secrets.*`, `secret.*`, `service-account*.json`, `firebase-adminsdk*.json`, `kubeconfig`, `*.kubeconfig`

When private files are discovered by name, do not call out their exact paths in the generated README. Use a general note such as "private configuration files are intentionally excluded from documentation" instead of writing "docker/deploy/.env contains sensitive information".

Safe examples may be read if they exist and are clearly examples:

- `.env.example`, `.env.sample`, `.env.template`
- `application-example.yml`, `application-example.yaml`
- `config.example.*`, `settings.example.*`

### Recommended Scan Commands

Use the platform's fastest available search tool. If `rg` is unavailable, use native shell alternatives.

1. Project structure, max depth 4, with excludes for secret files and build output.
2. Manifest files only:
   - Node: `package.json`, `pnpm-lock.yaml`, `yarn.lock`, `package-lock.json`, `vite.config.*`, `next.config.*`, `nuxt.config.*`, `tsconfig.json`
   - Python: `pyproject.toml`, `requirements*.txt`, `setup.py`, `setup.cfg`, `Pipfile`, `poetry.lock`, `uv.lock`
   - Java/Kotlin: `pom.xml`, `build.gradle`, `build.gradle.kts`, `settings.gradle`, `gradle.properties`, `src/main/resources/application*.yml`, `src/main/resources/application*.yaml`, excluding private profiles listed above
   - Go: `go.mod`, `go.sum`, `Makefile`, `Taskfile.yml`
   - Shared: `Dockerfile`, `docker-compose*.yml`, `.github/workflows/*`, `.gitlab-ci.yml`, `LICENSE`, `CHANGELOG.md`, `CONTRIBUTING.md`, `docs/**`
3. Entry points and routes:
   - read only source files likely to define startup, CLI, routing, or public APIs.
   - avoid scanning generated files, minified bundles, compiled output, and vendored dependencies.
4. Existing docs:
   - check `README.md`, `README.zh-CN.md`, `README.en.md`, `docs/`, `CHANGELOG.md`, `LICENSE`.
5. Git metadata:
   - repo URL and recent commit subjects may be used only as weak context; never invent features from commit titles alone.

## Step 2: README Existing-File Branch

Before writing, determine the target file(s):

- `zh`: `README.md` in Chinese, unless the user requests `README.zh-CN.md`.
- `en`: `README.md` in English, unless the user requests `README.en.md`.
- `both`: generate separate `README.zh-CN.md` and `README.en.md`. Optionally generate a short `README.md` index only when no `README.md` exists or the user approves.
- no argument: infer the primary language from existing docs/user request. If the user asks for bilingual docs or the project is meant for both audiences, use `both`.

If any target file already exists:

1. Stop before writing that file.
2. Tell the user which file exists.
3. Ask whether to:
   - overwrite it,
   - create a separate file such as `README.generated.md`, `README.zh-CN.md`, or `README.en.md`,
   - merge selected content into the existing README.
4. Continue only after the user chooses, unless the user already gave explicit overwrite permission.

## Step 3: Language And Project-Type Detection

Detect the implementation language before writing. When multiple languages exist, identify the role of each one instead of forcing a single label.

### Node.js / JavaScript / TypeScript

Signals:

- `package.json`, `vite.config.*`, `next.config.*`, `nuxt.config.*`, `tsconfig.json`
- `src/main.ts`, `src/index.ts`, `server.ts`, `app.ts`, `pages/`, `app/`, `src/routes/`

README handling:

- Use package manager from lockfile: `pnpm-lock.yaml` → `pnpm`, `yarn.lock` → `yarn`, `package-lock.json` → `npm`.
- Extract only real scripts from `package.json`.
- Separate frontend and backend when both exist.
- Ignore `dist/`, `build/`, `.next/`, `.nuxt/`, `out/`, and coverage output.
- For frontend projects, emphasize dev/build/preview commands, environment example files, and public configuration.
- For backend Node projects, document start/test/lint scripts, server entry point, routes, and runtime requirements.

### Python

Signals:

- `pyproject.toml`, `requirements*.txt`, `setup.py`, `Pipfile`, `poetry.lock`, `uv.lock`
- `main.py`, `app.py`, `manage.py`, `wsgi.py`, `asgi.py`, `src/`, package modules

README handling:

- Detect tooling: `uv`, Poetry, Pipenv, pip/venv.
- For FastAPI/Flask/Django, document the actual command style only when found in files or scripts.
- For libraries, include install/import usage only when package metadata or examples exist.
- Avoid claiming model, database, queue, or cloud integrations unless code/config proves them.

### Java / Kotlin

Signals:

- `pom.xml`, `build.gradle`, `build.gradle.kts`, `settings.gradle`
- `src/main/java`, `src/main/kotlin`, `src/main/resources`

README handling:

- Detect Maven vs Gradle and use the matching commands.
- Identify framework only from dependencies or code annotations, such as Spring Boot, Quarkus, Micronaut.
- Ignore `target/`, `build/`, `.gradle/`, `classes/`, and generated sources.
- Do not read private Spring profile files such as `application-prod.yml` or `application-local.yml`; read safe example/default config only.
- Document Java version only if declared in build files.

### Go

Signals:

- `go.mod`, `cmd/**/main.go`, `main.go`, `internal/`, `pkg/`

README handling:

- Use module path from `go.mod`.
- Document commands such as `go run`, `go build`, and `go test ./...` only when they fit the detected entry point.
- For CLI tools, include command examples only when flags/examples are discoverable from code or docs.
- For services, document route/API details only from explicit router definitions or OpenAPI files.

### Frontend / Backend / Full-Stack Classification

- Frontend: UI framework config, browser entry files, static assets, routes/pages, no server entry.
- Backend: server entry, API routes/controllers, database/migration folders, no browser UI.
- Full-stack: both frontend and backend signals, monorepo workspaces, or separate `client/` and `server/` directories.

Document full-stack projects with clear subsections:

- Frontend
- Backend
- Shared configuration
- Local development flow

## Step 4: API Scanning Rules

Only include an API section when API evidence exists.

Accepted evidence:

- OpenAPI/Swagger files: `openapi.yaml`, `openapi.yml`, `swagger.json`, `api-docs.*`
- Route/controller definitions:
  - Express/Koa/Fastify route calls
  - Next.js/Nuxt server routes
  - FastAPI decorators, Flask blueprints, Django urls/views
  - Spring `@RequestMapping`, `@GetMapping`, `@PostMapping`, etc.
  - Go router registrations from common routers such as `net/http`, Gin, Echo, Chi, Fiber
- Existing docs or tests that explicitly call endpoints.

Useful search patterns:

- Node/Express/Fastify/Koa: `.get(`, `.post(`, `.put(`, `.patch(`, `.delete(`, `router.`, `fastify.route`
- Next/Nuxt server routes: `app/api/**`, `pages/api/**`, `server/api/**`, `server/routes/**`
- Python: `@app.get`, `@app.post`, `@router.`, `Blueprint(`, `urlpatterns`, `path(`, `re_path(`
- Java/Kotlin: `@RestController`, `@Controller`, `@RequestMapping`, `@GetMapping`, `@PostMapping`, `@PutMapping`, `@DeleteMapping`, `@PatchMapping`
- Go: `http.HandleFunc`, `.HandleFunc`, `.GET(`, `.POST(`, `.PUT(`, `.PATCH(`, `.DELETE(`, `router.Handle`

Rules:

- Extract method and path only when both are explicit.
- Include handler/controller name when obvious.
- Do not infer request/response bodies unless schema, DTO, type, validation model, or docs define them.
- Do not guess authentication, roles, rate limits, database side effects, or error codes.
- If endpoints are numerous, show only core groups and point to the source/OpenAPI file.
- If route construction is dynamic and unclear, write a short note: "接口由运行时代码组装，README 中只列出仓库中可直接确认的入口。"

Preferred compact table:

```markdown
| Method | Path | Source | Notes |
|--------|------|--------|-------|
| GET | `/api/users` | `src/routes/users.ts` | User list endpoint |
```

## Step 5: README Structure

Only include sections with meaningful evidence. A good README usually contains:

```markdown
# Project Name

> One-line project summary grounded in manifest/docs/code.

## Overview

## Features

## Tech Stack

## Project Structure

## Getting Started

### Prerequisites
### Installation
### Configuration
### Run
### Test

## API

## Deployment

## Development Notes

## Security And Privacy

## License
```

Skip empty sections. Do not include placeholder copy such as `TODO`, `TBD`, or "coming soon".

## Step 6: Structure And Architecture Diagrams

### Directory Tree

Generate a compact tree:

- max depth 3 unless a deeper level is essential.
- max 35 lines.
- show source, config, tests, docs, deployment files, and manifests.
- omit build output, dependencies, generated code, and private config files.

### Mermaid Architecture

Include a Mermaid diagram only when the repository clearly shows multiple components or layers.

Rules:

- Do not draw databases, queues, cloud services, model providers, external APIs, or microservices unless they are explicitly present in dependencies/config/code/docs.
- Prefer "request flow" or "module relationship" diagrams over grand architecture maps.
- If evidence is weak, omit the diagram and keep the tree.
- Keep diagrams small: 5-9 nodes.

## Step 7: Security, Privacy, And License Voice

Use first-person maintainer language and avoid generic AI-sounding advice.

Bad style:

```markdown
生产环境建议 LANGSMITH_CAPTURE_CONTENT=false，避免患者文本外传。
模型 API Key 和数据库密码通过环境变量注入，不要硬编码。
建议为镜像拉取创建只读账号，不要共享个人主账号。
```

Better Chinese style:

```markdown
## 安全与隐私

我不会把本地 `.env`、密钥文件或生产配置写进 README，也不会在文档中复述这些文件的内容。仓库目前只适合记录示例配置；真实凭据请继续放在部署环境或本机私有配置中。
```

Better English style:

```markdown
## Security And Privacy

I keep local `.env` files, key files, and production-only configuration out of this README. This repository should document example configuration only; real credentials belong in the deployment environment or local private config.
```

License handling:

- If a license file exists, name it accurately.
- If no license file exists, do not give legal advice and do not pressure the user.
- Use first-person, concise wording:

```markdown
## License

我还没有在仓库中放置许可证文件；在补充 `LICENSE` 之前，这个项目默认只按仓库当前权限使用。
```

```markdown
## License

I have not added a license file yet. Until `LICENSE` is added, use this project only under the repository's current access permissions.
```

## Step 8: Output Length Control

Keep README output practical:

- target length: 120-220 lines for normal projects.
- hard limit: 300 lines unless the user requests exhaustive documentation.
- max 8 features.
- max 12 tech stack rows.
- max 35 directory tree lines.
- max 20 API rows; group or link to source when larger.
- max 8 commands across install/run/test/build/deploy unless the project explicitly needs more.
- avoid printing the full generated README in chat if it is long; summarize changed files and key sections instead.

## Step 9: Bilingual Documentation

When generating both Chinese and English:

- create separate files: `README.zh-CN.md` and `README.en.md`.
- keep the two versions equivalent in structure and facts.
- do not machine-translate awkwardly; localize section names and command descriptions naturally.
- avoid mixing Chinese and English paragraphs in the same file except for code, commands, package names, and standard technical names.
- if creating or updating `README.md`, make it a short index linking to both language versions, unless the user asks for one language as the primary README.

Recommended `README.md` index:

```markdown
# Project Name

- [中文文档](./README.zh-CN.md)
- [English Documentation](./README.en.md)
```

## Quality Checklist

Before writing or finalizing, verify:

- [ ] No excluded private files were read or summarized.
- [ ] Existing README targets were checked and overwrite permission was handled.
- [ ] Project language and project type were detected before generation.
- [ ] Commands come from manifests, build files, docs, or clear framework conventions.
- [ ] API entries are backed by explicit route/OpenAPI evidence.
- [ ] Directory tree matches real files and excludes build/dependency output.
- [ ] Architecture claims are not invented.
- [ ] Security and license notes use first-person maintainer voice.
- [ ] Chinese and English docs are factually aligned when both are generated.
- [ ] The README is concise and contains no placeholders.
