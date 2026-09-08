# Evidence And Repository Scan

Read this reference before scanning a project for README generation.

## Safe Boundaries

Never read, grep, or display content from:

- VCS internals: `.git/`, `.svn/`, `.hg/`;
- dependency and environment directories: `node_modules/`, `vendor/`, `.venv/`, `venv/`, `env/`;
- generated output and caches: `dist/`, `build/`, `target/`, `coverage/`, `.next/`, `.nuxt/`, `out/`, `.gradle/`, `__pycache__/`;
- logs and data dumps: `*.log`, `logs/`, `*.dump`, `*.sql`, `*.sqlite`, `*.db`;
- private configuration: `.env`, `.env.*`, `*.env`, `application-local.*`, `application-prod.*`, `bootstrap-prod.*`, `settings.local.*`, `local_settings.*`;
- credentials: `*.pem`, `*.key`, `*.p12`, `*.pfx`, `id_rsa*`, `id_ed25519*`, `credentials.*`, `secrets.*`, `secret.*`, `service-account*.json`, `kubeconfig`.

Safe examples such as `.env.example`, `.env.sample`, `config.example.*`, and `application-example.*` may be read. Do not mention the exact location of private files in the generated README.

## Scan Order

1. Existing docs: README variants, `docs/`, changelog, contributing guide, license.
2. Manifests and lockfiles: identity, scripts, direct dependencies, supported versions.
3. Entry points: app bootstrap, CLI main, server startup, exports.
4. Configuration examples and typed settings models.
5. Routes or API specifications.
6. Tests, deployment files, and source layout where they clarify public behavior.

Search narrowly after the first pass. Avoid reading every source file when a manifest, explicit registration, or maintained reference already answers the question.

## Ecosystem Signals

Use the project's own toolchain and terminology.

| Ecosystem | Identity and command sources |
|-----------|------------------------------|
| Node.js / TypeScript | `package.json`, lockfile, workspace file, framework config |
| Python | `pyproject.toml`, `requirements*.txt`, lockfile, CLI entry points |
| Java / Kotlin | `pom.xml`, Gradle files, framework configuration, application entry point |
| Go | `go.mod`, `cmd/`, `main.go`, explicit flag and router registration |
| Rust | `Cargo.toml`, `src/main.rs`, `src/lib.rs`, argument definitions |
| .NET | solution and project files, `Program.cs`, launch settings examples |
| Ruby | `Gemfile`, gemspec, `Rakefile`, Rails entry points |
| PHP | `composer.json`, `artisan`, framework console or public entry point |
| Elixir | `mix.exs`, application supervision tree, Phoenix routes |
| C / C++ | CMake, Make, Meson, configure files, executable targets |
| Swift | `Package.swift`, Xcode project/workspace, executable targets |
| Dart / Flutter | `pubspec.yaml`, `lib/main.dart`, platform configuration |
| Zig | `build.zig`, source entry points |
| Shell | executable scripts, Make targets, documented environment assumptions |

For mixed projects, identify each ecosystem's role. For monorepos, find the independently runnable packages and document one top-level path before package-specific paths.

## Evidence Rules

- Detect the package manager from the repository's lockfile or explicit package manager field.
- Extract commands from real scripts, targets, or maintained project docs. A familiar convention is not evidence.
- Treat dependency versions and runtime versions as different facts. A lockfile rarely proves the required runtime version.
- Include direct technologies only when readers need them to install, integrate, operate, or contribute.
- Derive configuration keys from example files, schemas, settings models, or explicit lookups. Never expose real values.
- Record an API method and path only when both are explicit. Do not infer auth, schemas, errors, or rate limits.
- A `Dockerfile` proves a build path, not a registry name, production deployment, or cloud provider.
- A test directory proves tests exist, not that a guessed test command works.
- Existing README prose is evidence of maintainer intent, but reconcile it with current manifests and source before repeating operational facts.

Use a source reference in the generated README when it helps the reader verify or navigate. Source references are optional for obvious setup prose; they are valuable for API tables, compatibility claims, benchmarks, and unusual constraints.
