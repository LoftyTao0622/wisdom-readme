# README Design And Structure

Read this reference when creating a README, changing its visual identity, choosing among several reader paths, or deciding whether media and diagrams help.

## Design By Project Character

### Minimal

Use for libraries, infrastructure, standards, source repositories, and projects with strong external documentation.

Typical flow:

```text
identity → positioning → essential links → why/use cases → quick start → contribution/license
```

Use a logo only when the repository already owns one. Keep badges limited to facts that build trust or affect adoption. Rust and shadcn/ui show that a strong README can be short when it sends readers to the right maintained docs.

### Product

Use for applications and tools whose value becomes clear through an interface, output, or observable workflow.

Typical flow:

```text
identity → outcome → proof image/demo → primary action → capabilities → deeper docs
```

Choose one hero asset. A screenshot should show the real result, a benchmark should link to its method, and a demo should lead to a stable project-owned destination. uv's benchmark visual works because it supports the product promise rather than filling space.

### Editorial

Use for creative tools, curated repositories, educational projects, and work whose point of view matters.

Typical flow:

```text
identity → concise thesis → selected highlights → guided journey → context and credits
```

Let headings, sentence rhythm, and whitespace carry the style. Use fewer badges and tables. Avoid a wall of equally weighted features; select the ideas that define the project.

### Reference-led

Use for SDKs, APIs, CLIs, and mature tools with several common workflows.

Typical flow:

```text
identity → exact scope → choose a path → minimal working example → task reference → full docs
```

A compact path selector is useful when readers arrive with different goals. Playwright's “Best for / Install” table is a strong pattern: it resolves the first decision before expanding each workflow.

## Opening Composition

The opening needs three things: identity, meaning, and direction.

- **Identity:** project name; optional project-owned logo or mark.
- **Meaning:** one concise sentence stating what it is, who it serves, and the outcome.
- **Direction:** the primary documentation, demo, install command, or path selector.

Badges are metadata. Add them when they answer a real adoption question: package version, supported runtime, build health, license, or community entry point. Verify each destination and status source. Use one badge style and keep the group visually quiet.

Choose alignment deliberately. Left alignment reads as technical and direct. Centered composition suits an established logo or product hero. Do not center long prose, setup instructions, tables, or reference material.

Markdown cannot control typography reliably across hosts. Create hierarchy through short headings, paragraph length, code examples, whitespace, and the order of information. Use HTML sparingly for a header, responsive `<picture>`, or image sizing; important content must remain readable in plain Markdown.

## Natural Writing

- Begin a section with its useful claim or action. Do not announce what the section will discuss.
- Prefer concrete outcomes over adjectives: “opens an interactive API explorer at `/docs`” carries more information than “powerful and intuitive.”
- Mix short orienting sentences with slightly longer explanations. Repetitive one-line bullets make a README feel machine-produced.
- Use bullets for parallel choices and tables for exact comparisons. Use prose when one idea leads to the next.
- Keep one term for each concept. Match names used by the product and repository.
- Use bold to reveal scan structure, not to decorate every sentence.
- Avoid excessive emoji, ornamental dividers, nested callouts, animated assets, and badges that restate the prose.

## Proof Before Detail

Choose the smallest artifact that makes the main promise believable:

- a minimal working code example for a library;
- a short terminal session for a CLI;
- a real screenshot for an application;
- a sourced benchmark for a performance tool;
- a small diagram for a multi-component service;
- a curated example link for a collection.

One strong proof is usually enough above the first setup path. Give images descriptive alt text and concise captions. Support light and dark variants with `<picture>` only when both assets exist.

For an experiential API or framework README, the sequence “create → run → observe” can teach more effectively than a long feature list. FastAPI demonstrates this by carrying one example through code, server startup, response, and interactive docs.

## Structural Patterns

Use these as starting points, then remove irrelevant sections.

### Library Or SDK

```text
Positioning
Installation
Minimal example
Common tasks
Compatibility or configuration
API documentation
Contributing and license
```

### Application Or Service

```text
Positioning and real interface image when available
Primary local run path
Configuration
Architecture when it clarifies dependencies
Operations or deployment when verified
Contributing and license
```

### CLI

```text
Positioning and one representative invocation
Installation
Common workflows
Command reference or --help link
Configuration
Contributing and license
```

### Monorepo Or Multi-Product Tool

```text
Shared positioning
Choose-your-path table
One recommended top-level setup
Package or product paths
Shared development workflow
Contributing and license
```

### Source Repository Or Documentation Hub

```text
Repository identity and scope
Why it exists
Quick link to the normal user installation path
Source-build or contribution links
Help, governance, license, trademark when applicable
```

Keep contributor setup out of the primary user path unless contributors are the main audience. Link detailed API, operations, and contribution material rather than duplicating it.

### Skill Or Prompt Package

Reusable skills need two entry points when both are supported:

```text
identity → capability boundary → example or prompt → install/use path → adjustable parameters → invariants → file map
```

Show the host-assistant path first, then the direct-prompt path. A short “adjustable parameters” table makes the package feel configurable without weakening its core behavior. Follow it with two or three invariants that protect provenance, safety, or output quality. For platform copies, identify the editing source and the synchronization rule so maintainers know where a change belongs.

### Intelligent Navigation

Make branching explicit instead of stacking equal-weight links. A compact table works well when readers choose by goal:

| If you want to… | Start here | You will get |
|----------------|------------|--------------|
| Try the default path | Quick Start | A first observable result |
| Adapt the output | Parameters | The supported controls and trade-offs |
| Understand the method | How it works | The evidence and decision sequence |
| Maintain the package | Structure / maintenance | Source files and synchronization steps |

Use this only when the repository has genuinely different paths. Otherwise keep the opening linear.

## Responsive And Accessible Presentation

- Keep tables compact; move paragraphs below them when cells become dense.
- Let badges wrap naturally and keep labels short.
- Use descriptive link text and meaningful image alt text.
- Avoid color as the only carrier of meaning.
- Do not depend on fixed pixel widths for the whole layout.
- Provide text instructions for any action demonstrated through an image or animation.
- Prefer repository-relative links for maintained files and assets.

## Open-Source References

Use these projects as structural references, not as templates or evidence about another project:

- [Playwright](https://github.com/microsoft/playwright/blob/main/README.md) — early path selection for multiple products and workflows.
- [uv](https://github.com/astral-sh/uv/blob/main/README.md) — a proof visual tied to the core promise, followed by highlights and installation.
- [FastAPI](https://github.com/fastapi/fastapi/blob/master/README.md) — product identity and an end-to-end create/run/observe example.
- [Rust](https://github.com/rust-lang/rust/blob/main/README.md) — a concise source-repository hub that routes users to maintained guides.
- [shadcn/ui](https://github.com/shadcn-ui/ui/blob/main/README.md) — restrained positioning and a direct path to maintained documentation.
