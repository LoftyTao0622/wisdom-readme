<div align="center">

<sub><strong>AI CODING ASSISTANT SKILL&nbsp;&nbsp;·&nbsp;&nbsp;DOCUMENTATION SYSTEM</strong></sub>

# generate-readme

从真实仓库证据出发，生成严谨、可执行、以读者为中心的 README。

<a href="./README.zh-CN.md"><img src="https://img.shields.io/badge/中文-README-C2415A?style=flat-square&labelColor=F6E7EA" alt="中文 README"></a>
<a href="./README.en.md"><img src="https://img.shields.io/badge/English-README-2F6F68?style=flat-square&labelColor=E3F0EE" alt="English README"></a>
<img src="https://img.shields.io/badge/14_ecosystems-supported-6B5B95?style=flat-square&labelColor=EEEAF4" alt="14 ecosystems supported">
<img src="https://img.shields.io/badge/evidence--backed-documentation-D28A3D?style=flat-square&labelColor=F7EEDD" alt="Evidence-backed documentation">

<p>
  <a href="./README.zh-CN.md">中文文档</a>
  <span> · </span>
  <a href="./README.en.md">English Documentation</a>
</p>

</div>

## Quick Reference

| Argument | Output |
|----------|--------|
| `zh` | Chinese README |
| `en` | English README |
| `<locale>` | Any language (e.g., `ja`, `fr`, `ko`) |
| `both` | `README.zh-CN.md` + `README.en.md` |
| omitted | Inferred from user's request |

## Trigger

```text
生成中文 README
create a readme for this repository
generate readme language: both
```

## Install

Copy `SKILL.md` into your assistant's skills directory (`.claude/skills/generate-readme/`, `.codex/skills/generate-readme/`, etc.).

## License

[Apache License 2.0](LICENSE)
