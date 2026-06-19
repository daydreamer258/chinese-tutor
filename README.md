# Chinese Tutor - 高考语文辅导

> 创建：2026-06-19
> 版本：v1.0

## 目录结构

```
chinese-tutor/
├── knowledge/           # 知识库（静态，可迭代更新）
│   ├── exam-syllabus.md         # 考纲与命题趋势
│   ├── classical-chinese.md     # 文言文体系（实词/虚词/句式/断句/翻译）
│   ├── poetry-appreciation.md   # 诗歌鉴赏（意象/手法/情感/模板）
│   ├── modern-reading.md        # 现代文阅读（论述类/文学类/实用类）
│   ├── composition.md           # 作文指导（审题/立意/结构/诊断）
│   ├── language-usage.md        # 语言文字运用（成语/病句/得体/连贯）
│   └── diagnosis.md             # 教学诊断方法论
├── skills/              # 技能文件
│   ├── chinese-tutor-teach.md   # 核心教学技能
│   └── chinese-tutor-update.md  # 知识库迭代更新技能
├── prompts/             # Prompt 文件
│   └── chinese-tutor.md         # 专属 system prompt
└── README.md
```

## 设计原则

1. **项目级隔离**：本目录在 `workspace/chinese-tutor/` 下，仅 chinese-tutor agent 加载
2. **知识库可迭代**：通过 `chinese-tutor-update` 技能，支持根据用户反馈更新 knowledge 文件
3. **教学诊断驱动**：不只是答题机器，会根据学生错误类型做针对性辅导
4. **高考导向**：所有内容围绕高考语文考纲和新高考趋势设计

## 模块说明

| 模块 | 内容概要 | 高考对应分值 |
|------|---------|------------|
| 考纲与命题 | 卷面结构、近五年趋势、2026备考方向 | 全卷 150 分 |
| 文言文 | 120实词+18虚词+特殊句式+断句翻译 | ~19 分 |
| 诗歌鉴赏 | 意象+手法+情感+答题模板 | ~9 分 |
| 现代文阅读 | 三类文本+选择题技巧+主观题模板 | ~35 分 |
| 作文 | 审题立意+结构框架+高分技巧+问题诊断 | 60 分 |
| 语言文字运用 | 成语+病句+得体+连贯 | ~20 分 |
| 诊断 | 五维诊断框架+按板块处方 | 教学元能力 |
