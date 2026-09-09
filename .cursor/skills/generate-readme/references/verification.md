# README Verification

Read this after a substantial README creation or rewrite. Fix failures before reporting completion.

## Evidence Pass

Trace consequential claims across the opening, prose, badges, tables, examples, and diagrams.

- Commands exist in scripts, build files, maintained docs, or explicit executable behavior.
- Versions come from the correct source: runtime requirements from runtime declarations, package versions from package metadata.
- External services appear in direct dependencies, configuration, or deployment definitions.
- API methods and paths match route definitions or the API specification.
- Configuration names and purposes match examples, schemas, models, or explicit lookups; no secret values appear.
- Architecture labels reflect real components and relationships.
- Performance and comparison claims link to reproducible or project-owned evidence.
- Badge labels and destinations agree with repository facts.
- Technology-stack badges represent primary, declared components rather than merely transitive lockfile packages; runtime and version claims come from the appropriate declaration source.
- License wording matches a license file or explicit manifest metadata.
- Multilingual files describe the same behavior and constraints.

Remove or narrow any claim that cannot be traced confidently.

## Reader Pass

Read from the top without relying on prior repository knowledge.

- The opening explains the project and intended reader in plain language.
- The main promise becomes concrete through an example, result, or precise capability.
- The primary next action is visible and coherent.
- Alternative paths are easy to compare and visibly secondary to the recommended path.
- Prerequisites, working directory, shell differences, downloads, and external services appear where they affect success.
- The first example is understandable and runnable.
- Headings alone reveal a sensible journey.
- Detailed reference and maintainer material does not interrupt the first-use path.

## Presentation Pass

- Heading levels are consistent and no section is empty.
- Paragraphs, lists, tables, code, and media form a varied but calm rhythm.
- Badges, bold text, emoji, callouts, and separators are restrained; any emoji or icon-led heading adds wayfinding and remains understandable as text.
- One visual element clearly leads; multiple decorative elements do not compete.
- Tables remain readable on narrow screens.
- Code fences use an appropriate language identifier.
- Images have useful alt text and do not carry essential instructions alone.
- Internal file links and heading anchors resolve; external links use stable, descriptive destinations.
- Light and dark assets render correctly when responsive `<picture>` markup is used.

## Voice Pass

- The prose sounds like one maintainer with a clear point of view.
- There is no AI self-reference or scan narration.
- Claims use concrete language instead of unsupported superlatives.
- Sentence openings and bullet forms are not mechanically repetitive.
- There are no placeholders, generic best-practice paragraphs, duplicated explanations, or stale future-tense promises.

## Useful Checks

Use repository-native checks when available. For Markdown itself, useful lightweight checks include:

- search for `TODO`, `TBD`, `coming soon`, and AI self-reference;
- inspect all relative links and image paths;
- compare documented commands with manifests and scripts;
- render or preview the README when HTML, tables, responsive images, or complex diagrams are present.

Do not declare success based only on a linter. The final reader pass is required because structure, tone, and visual balance are editorial judgments.
