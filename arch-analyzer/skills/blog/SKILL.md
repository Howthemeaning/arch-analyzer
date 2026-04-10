---
name: arch-blog
description: 基于分析结果生成可发布的技术博客，自动引用 Mermaid 图表，并进行自我审查。
allowed-tools: Read, Write, Edit, Task, AskUserQuestion
---

# Technical Blog Generator

## 目标

- 基于分析结果生成高质量技术博客
- 自动引用 PLAN.md 和 Mermaid 图表
- 进行自我审查，确保内容质量
- 输出可直接发布的技术博客

## 执行原则

1. 必须依赖 `/analysis` 的输出，先检查分析产物存在
2. 图表引用是硬步骤，必须正确嵌入 Mermaid 代码
3. 自我审查不可跳过
4. 审查不通过必须修订

## 输出位置

**所有产物生成在被分析的目标项目目录下**：

```text
target-project/
└── blogs/
    ├── .blog-state.json         # 博客状态文件
    ├── YYYY-MM-DD-topic-slug.md # 博客文章
    └── drafts/                  # 草稿目录
        └── topic-draft.md
```

## 前置依赖

必须先执行 `/analysis`，检查以下文件存在：
- `PLAN.md`
- `analysis/difficulties.json`
- `analysis/diagrams/`

若不存在，提示用户先执行 `/analysis`。

## References 加载等级

- L0：未进入对应步骤前，不加载任何参考文件
- L1：每步仅加载该步"必读"文件
- L2：仅在触发条件满足时加载"条件必读"文件

## References 清单

- `references/blog-template.md`：博客结构模板，Step 3 必读
- `references/writing-style.md`：写作风格指南，Step 4 必读
- `references/review-checklist.md`：审查清单，Step 5 必读

## 工具策略

- `Read`：读取 PLAN.md、difficulties.json、图表文件
- `Write/Edit`：生成博客文件
- `Task`：调用 blog-writer-agent
- `AskUserQuestion`：选题确认、审查结果裁决

## 交互流程

### Step 0：预检

检查内容：
- `PLAN.md` 存在
- `analysis/difficulties.json` 存在
- `analysis/diagrams/` 目录存在

若缺失，提示：`请先执行 /analysis 命令生成分析报告`

### Step 1：加载分析结果

读取内容：
- `PLAN.md`：项目概览、架构信息
- `analysis/difficulties.json`：技术难点清单
- `analysis/diagrams/*.md`：所有 Mermaid 图表

### Step 2：选题筛选

从 difficulties.json 中筛选适合博客的选题：

筛选标准：
- `blog_potential: "high"` 优先
- 有具体代码位置
- 有足够的技术深度
- 可引用现有图表

输出：
- 选题列表（最多5个候选）
- 使用 AskUserQuestion 让用户选择

### Step 3：大纲生成

加载参考：
- `references/blog-template.md`

大纲结构：
```markdown
# [标题]

## 背景
- 问题来源
- 为什么重要

## 问题分析
- 技术难点描述
- 相关架构图

## 解决方案
- 核心思路
- 实现细节
- 代码示例

## 效果与总结
- 解决效果
- 经验总结
```

### Step 4：内容撰写

加载参考：
- `references/writing-style.md`

撰写要求：
- 引用 PLAN.md 中的相关内容
- 嵌入 Mermaid 图表代码（从 diagrams/ 读取）
- 提供代码示例（从源文件提取）
- 字数控制在 2000-5000 字

图表引用方式：
```markdown
### 架构图

```mermaid
[从 diagrams/system-architecture.md 复制的 Mermaid 代码]
```
```

### Step 5：自我审查

加载参考：
- `references/review-checklist.md`

审查项目：
- [ ] 标题是否吸引人且准确
- [ ] 技术难点描述是否清晰
- [ ] Mermaid 图表是否正确嵌入
- [ ] 代码示例是否准确
- [ ] 文章结构是否完整
- [ ] 语言是否流畅、专业
- [ ] 字数是否在合理范围

评分标准：
- 85分以上：通过
- 70-85分：建议修订
- 70分以下：必须修订

### Step 6：修订内容

若审查不通过：
- 根据审查意见修订
- 重新执行 Step 5 审查
- 最多修订2轮

### Step 7：保存博客

文件命名：`YYYY-MM-DD-topic-slug.md`
- 日期：当前日期
- slug：从标题生成（英文、小写、连字符）

保存位置：`blogs/YYYY-MM-DD-topic-slug.md`

更新状态：`blogs/.blog-state.json`

## 输出格式规范

### 博客文件结构

```markdown
# [标题]

> 作者：[可选]
> 发布日期：YYYY-MM-DD

## 背景

[问题描述]

## 问题分析

### 技术难点

[难点描述]

### 相关架构

```mermaid
[Mermaid 图表代码]
```

## 解决方案

### 核心思路

[方案概述]

### 实现细节

[详细实现]

```[language]
[代码示例]
```

## 效果与总结

[总结内容]

---

**相关文件**：
- [PLAN.md](../PLAN.md) - 项目完整分析报告
- [架构图](../analysis/diagrams/system-architecture.md)
```

### .blog-state.json

```json
{
  "last_blog": "2026-04-10-distributed-transaction.md",
  "total_blogs": 3,
  "blogs": [
    {
      "file": "2026-04-10-distributed-transaction.md",
      "title": "深入理解分布式事务处理",
      "topic_id": "diff-001",
      "word_count": 3500,
      "review_score": 88,
      "diagrams_used": ["system-architecture", "data-flow"],
      "created_at": "2026-04-10"
    }
  ]
}
```

## 质量标准

- [ ] 博客结构完整
- [ ] 至少引用1个 Mermaid 图表
- [ ] 审查评分 >= 85
- [ ] 字数在 2000-5000 范围
- [ ] 文件命名规范