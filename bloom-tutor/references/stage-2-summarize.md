# Stage 2: Knowledge Extraction And Summary

Use this stage when the user asks for a summary, recap, knowledge points, or what they learned.

## Loaded Skills

- `knowledge-extraction`
- `solo-assessment`
- `markdown-formatter`

## Goal

Turn the dialogue into reusable knowledge with explicit structure.

## Flow

1. Review the problem-solving process.
2. Extract the 3-5 most important concepts, methods, or insights.
3. Map each concept to a Bloom level.
4. Assess the user's current SOLO level.
5. Provide a structured summary and the next-step prompt.

## Knowledge Card Template

| 核心概念 | 我的理解 | 应用场景 | 关联旧知 | 布鲁姆层级 |
| --- | --- | --- | --- | --- |
| [概念 1] | [优先引用用户原话并适度整理] | [何时使用] | [与什么相关] | [记忆/理解/应用/分析/评价/创造] |
| [概念 2] | [用户的当前理解] | [何时使用] | [与什么相关] | [层级] |

## SOLO Assessment

Use these levels:

- `单点结构`: 只能识别一个方面
- `多点结构`: 能识别多个方面但无关联
- `关联结构`: 能建立点与点的联系
- `抽象扩展`: 能迁移到新场景或抽象出更通用原则

Use this output block after the summary table:

```text
【SOLO 评估】
当前层次: [层次名称]
判断依据: [引用或概括用户原话]
进阶建议: [给出一个具体问题或练习]
下一层次目标: [描述]
```

## Formatting Rules

- Always produce structured output in Stage 2.
- Prefer a table first, then a short list of reasoning steps or next actions.
- Keep the summary reusable; do not make it dependent on hidden context.
