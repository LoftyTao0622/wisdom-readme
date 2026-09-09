---
name: generate-readme
description: Create or revise project README files from repository evidence, with an appropriate information structure, natural maintainer voice, and restrained visual design. Use for README generation, rewrites, audits, localization, and README-focused documentation requests. Do not use for general documentation sets that do not include a README.
allowed-tools: [Read, Glob, Grep, Bash, Write]
---

# README Generator

Write the README that this project and its readers need. Ground every technical claim in the repository, make the first useful action obvious, and use visual design to clarify the content.

## Principles

Resolve conflicts in this order:

1. **Evidence** — include only claims, commands, versions, routes, and status signals supported by the repository or a project-owned source.
2. **User intent** — follow the requested language, file, scope, and degree of rewriting.
3. **Reader journey** — answer “What is this?”, “Is it for me?”, “How do I try it?”, and “Where do I go next?” in that order.
4. **Project identity** — preserve a coherent existing voice and visual system. When none exists, choose a presentation suited to the project instead of imposing a universal template.
5. **Restraint** — omit weak material. A short README with a clear purpose is better than a complete-looking document filled with generic sections.

## Workflow

### 1. Establish The Job

Read the existing README files, project description in manifests, top-level layout, and primary entry point. Form a one-sentence working statement that identifies:

- what the project is;
- who or what it serves;
- the outcome it enables.

Classify the primary reader action: install a library, run an application, invoke a CLI, consume a service, explore a collection, or contribute to a source repository. In mixed projects, select one primary path and expose other paths without making the opening compete with itself.

If the target README exists, infer the intended treatment:

- “improve”, “refresh”, or “update” means revise it in place;
- “rewrite” or “regenerate” permits replacement while preserving verified project-specific knowledge;
- ask about overwrite versus a separate file only when the request and destination remain materially ambiguous.

### 2. Build An Evidence Map

Before drafting, read [references/evidence-and-scan.md](references/evidence-and-scan.md). Apply its exclusions, inspect the relevant ecosystem signals, and keep a temporary ledger for consequential claims:

| Claim | Evidence | Confidence | Action |
|-------|----------|------------|--------|
| `npm run dev` starts the app | `package.json` scripts | Confirmed | Include |
| Production image is published | `Dockerfile` only | Unknown | Omit |

Use three confidence levels:

- **Confirmed** — explicit in source, manifest, configuration, or maintained project docs.
- **Derived** — a direct synthesis of confirmed facts with little interpretive risk.
- **Unknown** — suggested by convention, naming, stale prose, or incomplete code.

State confirmed facts directly. Phrase derived facts narrowly. Exclude unknown claims from the README.

### 3. Choose The Reading Experience

For a new README, a visual redesign, or a project with several valid entry paths, read [references/design-and-structure.md](references/design-and-structure.md). Select a structure and visual mode from the project evidence:

- **Minimal** — libraries, infrastructure, standards, and source repositories whose detailed docs live elsewhere.
- **Product** — applications and developer tools with a real screenshot, demo, or outcome to show.
- **Editorial** — creative tools, curated collections, and projects where voice and sequencing carry the identity.
- **Reference-led** — APIs, SDKs, and mature tools whose readers arrive for exact commands or compatibility facts.

These modes guide hierarchy and rhythm; they are not templates. A README may combine two when the project clearly calls for it.

The opening must contain the project name and a concise positioning statement. Add badges, a logo, navigation, or a hero only when each improves orientation, trust, or recognition. Metadata never replaces the positioning statement.

#### Make the intelligence visible

Treat the README as a guided interface, not a report. Before drafting, write a small design brief with four decisions:

| Decision | Question | Evidence to capture |
|----------|----------|---------------------|
| Primary path | What should a new reader do first? | Install, run, invoke, or open a documented entry point |
| Proof object | What makes the promise believable fastest? | A real output, screenshot, diagram, benchmark, or complete example |
| Choice points | Where do readers need to branch? | Platform, language, deployment, or contributor path |
| Depth boundary | What belongs in linked detail? | Configuration, API reference, operations, and maintainer material |

Use the brief to create a visible path selector when more than one audience or workflow is real. Keep one route recommended and label alternatives by outcome. Do not make readers infer the difference from a list of technologies.

Give the README one proof object above the first setup path whenever the repository contains a trustworthy artifact. Prefer a real project asset or a reproducible output; use a small Mermaid diagram only when relationships are the proof. Every visual must have descriptive alt text and a text equivalent.

Borrow visual language from the project itself. A creative tool may use an editorial hero and an example gallery; a CLI may use a terminal transcript; a service may use an architecture flow. When the user names a reference README, inspect its visual grammar (including any emoji or icon-led labels) as inspiration, then adapt it to this repository’s identity and evidence rather than copying its content. Keep one dominant visual, quiet metadata, short paragraphs, and generous whitespace. Never add decoration to compensate for missing evidence. Use at most one semantic emoji or icon per heading or label segment. A compact metadata row may group a few distinct marks when each segment has a clear meaning or link. Keep the wording complete without the mark and carry the same vocabulary across localized files.

Use this editorial sequence when it fits:

1. **Orient** — identity, audience, outcome.
2. **Prove** — one concrete example, screenshot, benchmark, output, or small diagram.
3. **Activate** — the shortest verified path to a first success.
4. **Deepen** — configuration, reference, operations, contributing, and license.

### 4. Draft For Use

Write as the maintainer speaking to a capable new user. Use direct verbs, specific nouns, and varied sentence length. Avoid generic superlatives, repetitive bold-label bullets, AI self-reference, and narration about scanning the repository.

Keep the conceptual layers distinct:

- **Positioning** explains what the project enables and for whom.
- **Features** describe user-visible capabilities and outcomes.
- **Technology** records only tools that affect installation, integration, operation, or contribution.
- **Architecture** explains meaningful component relationships.
- **Project structure** helps contributors locate a small number of important areas.

Getting Started must provide one coherent path from prerequisite to observable success. Every command must be traceable to a manifest, script, Makefile, maintained project document, or explicit source behavior. State the working directory, shell, external service, or large download when it changes the result.

Use examples that are complete enough to teach the action. Keep the first example easy to understand without scrolling; move advanced variants into later sections, collapsible details, or dedicated docs. Do not shorten an example so aggressively that it stops being runnable.

Document APIs only from explicit route definitions or an OpenAPI specification. When the endpoint set is large, summarize useful groups and link to the authoritative reference instead of reproducing it.

Add a diagram only when relationships are harder to understand in prose. Label components by responsibility, and include external services only when they are explicitly configured. Add media only when it demonstrates the primary outcome; use meaningful alt text and ensure the same action remains available in text.

For skills and reusable prompts, document both operating modes when they exist: using the skill through the host assistant and opening the prompt/reference directly. Show one copy-ready request for each mode, then state the observable result. Put adjustable parameters in a compact table and keep immutable principles separate so readers know what is safe to change.

### 5. Localize Deliberately

Use separate files for separate languages. Keep facts, commands, and section intent aligned while writing natural prose in each language. Do not mirror sentence structure mechanically.

When no language is specified, infer it from the user's request, existing documentation, and likely audience. Keep code, commands, package names, and identifiers unchanged.

### 6. Verify Before Finishing

After a substantial creation or rewrite, read [references/verification.md](references/verification.md) and perform both passes:

1. trace technical claims back to evidence;
2. read the result as a newcomer and test the information hierarchy, first action, links, and tone.

Fix failures before reporting completion. Keep the evidence ledger outside the repository unless the user asks for an audit artifact.

## Non-Negotiable Constraints

- Do not read or expose credentials, private environment files, logs, database dumps, dependency directories, build output, or VCS internals.
- Do not invent badges, download counts, compatibility, performance, deployment status, API behavior, or license terms.
- Do not create empty, placeholder, or template-only sections.
- Do not copy implementation walkthroughs into the README when a linked developer document serves the reader better.
- Do not replace a useful project identity with a generic badge wall or decorative hero.
- If no license file or manifest license exists, state the absence factually and avoid legal advice.
