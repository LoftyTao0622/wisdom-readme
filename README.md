# generate-readme

[中文文档](./README.zh-CN.md) | [English Documentation](./README.en.md)

> A README generation skill for AI coding assistants — produces rigorous, reader-centric project documentation from real repository evidence.

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
