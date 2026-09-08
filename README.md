<div align="center">

<sub>DOCUMENTATION, WITH JUDGMENT</sub>

# generate-readme

从仓库事实出发，写出准确、自然、可以真正上手的 README。

[中文说明](./README.zh-CN.md) · [English](./README.en.md)

</div>

> 证据决定写什么，读者路径决定先写什么，审美决定如何取舍与留白。

## 使用

把 [`SKILL.md`](./SKILL.md) 和 [`references/`](./references/) 放入编码助手的 skill 目录，然后直接描述目标：

```text
使用 generate-readme，为当前项目生成中文 README。
保留现有品牌风格，只写能够从仓库验证的内容。
```

这个 skill 会先识别项目与主要读者，再选择适合的阅读结构；技术细节经过证据核对，视觉表达则根据项目性格选择简约、产品、编辑或参考型风格。

## 设计线索

| 读者时刻 | README 要完成的事 |
|----------|-------------------|
| 第一眼 | 说清项目是什么、为谁解决什么问题 |
| 第一次停留 | 用示例、界面、结果或图表证明价值 |
| 第一次行动 | 给出一条可验证、可完成的上手路径 |
| 深入阅读 | 把配置、参考、运维与贡献信息放到合适位置 |

完整的行为说明见 [中文文档](./README.zh-CN.md)。

## License

[Apache License 2.0](./LICENSE)
