<div align="center">

<sub>A README AUTHORING SKILL FOR AI CODING ASSISTANTS</sub>

# generate-readme

Turn repository evidence into documentation that is accurate, natural, and easy to act on.

[中文](./README.zh-CN.md) · [English](./README.en.md)

</div>

## Why It Exists

A good README is more than a directory tree, a stack list, and a row of badges. It helps readers decide whether a project fits their needs, makes the value concrete, and gives them a path to a first successful result.

`generate-readme` separates two decisions: repository evidence defines what can be said, while the character of the project shapes the narrative and presentation. The result should sound like a maintainer welcoming a capable new user, not a scan report.

## Quick Start

Copy [`SKILL.md`](./SKILL.md) and [`references/`](./references/) into your coding assistant's skill directory:

```text
.codex/skills/generate-readme/
├── SKILL.md
└── references/
```

Then ask for the outcome directly:

```text
Use generate-readme to rewrite this project's English README.
Lead with the shortest runnable path, preserve its visual identity,
and exclude claims that cannot be verified from the repository.
```

The skill can also produce Chinese, bilingual, or locale-specific documentation. Each language receives its own file, with equivalent facts and commands but naturally localized prose.

## How It Decides

| Stage | Question | Result |
|-------|----------|--------|
| Position | What is this, who is it for, and what does it enable? | One-sentence positioning |
| Evidence | Can every command, version, capability, and relationship be traced? | Temporary evidence map |
| Design | Which reading rhythm belongs to this project? | Structure and visual mode |
| Writing | How does the reader reach a first successful result? | One coherent primary path |
| Verification | Do the facts, links, voice, and presentation hold together? | Corrected README |

Evidence is labeled confirmed, derived, or unknown. Source code, manifests, example configuration, and maintained project docs support direct claims; conventions and incomplete implementations do not become facts through confident wording.

## Four Reading Modes

The skill does not treat a centered title and a badge row as a universal default. It selects or combines modes from the repository itself:

- **Minimal** suits libraries, infrastructure, and source repositories. It emphasizes positioning, essential links, and a short entry path.
- **Product** suits applications and developer tools. A real interface, output, or reproducible result provides proof.
- **Editorial** suits creative tools, curated collections, and educational projects. Headings, paragraph rhythm, and whitespace carry the identity.
- **Reference-led** suits APIs, SDKs, and multi-entry CLIs. Readers choose a path before moving into exact usage.

The usual rhythm is “orient → prove → activate → deepen,” but the skill does not create empty sections to satisfy a template. Its design reference draws on mature patterns from [Playwright](https://github.com/microsoft/playwright/blob/main/README.md), [uv](https://github.com/astral-sh/uv/blob/main/README.md), [FastAPI](https://github.com/fastapi/fastapi/blob/master/README.md), [Rust](https://github.com/rust-lang/rust/blob/main/README.md), and [shadcn/ui](https://github.com/shadcn-ui/ui/blob/main/README.md).

## Content Boundaries

The skill verifies installation, run and test commands, configuration, APIs, external services, and license information. It does not read or expose private environment files, credentials, logs, database dumps, dependency directories, build output, or VCS internals.

Visual elements appear only when they perform a job:

- badges answer real questions about versions, compatibility, build health, or licensing;
- screenshots, recordings, and benchmark charts demonstrate the primary value;
- Mermaid diagrams clarify component relationships that prose cannot express compactly;
- technology lists include only what affects installation, integration, operation, or contribution.

## Repository Layout

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

The root files are the editing source. `.agents/`, `.claude/`, `.codex/`, `.cursor/`, and `.trae/` contain installable platform copies.

## Maintenance

Update the root `SKILL.md` or the relevant reference first, then synchronize the platform copies. Run the validator supplied by skill-creator to check frontmatter, naming, and unfinished scaffold placeholders. Real project trials and editorial review remain necessary for content quality.

## License

[Apache License 2.0](./LICENSE)
