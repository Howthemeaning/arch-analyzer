---
name: arch-analysis
description: 深度分析项目代码，生成技术分析文档 PLAN.md 和 Mermaid 架构图。识别技术栈、架构模式、功能模块和技术难点。
allowed-tools: Read, Grep, Write, Edit, Bash, Task
---

# Project Analysis (Deep Mode)

## 目标

- 深度分析项目代码，识别技术栈、架构模式、功能模块
- 挖掘技术难点和亮点
- 生成 Mermaid 架构图、模块依赖图、数据流图
- 输出结构化分析报告 PLAN.md

## 执行原则

1. 先校验输入完整性，再进入分析流程
2. 图表生成是硬步骤，不可跳过
3. 参考资料严格按步骤按需加载
4. 分析结果必须可被 `/blog` 直接消费

## 输出位置

**所有产物生成在被分析的目标项目目录下**：

```text
target-project/
├── PLAN.md                     # 技术分析文档（主产物）
└── analysis/
    ├── .analysis-state.json    # 分析状态文件
    ├── tech-stack.json         # 技术栈信息
    ├── diagrams/               # Mermaid 图表目录
    │   ├── system-architecture.md
    │   ├── module-dependency.md
    │   └── data-flow.md
    ├── modules.md              # 功能模块分析
    ├── difficulties.json       # 技术难点清单
    └── summary.md              # 分析摘要
```

## References 加载等级

- L0：未进入对应步骤前，不加载任何参考文件
- L1：每步仅加载该步"必读"文件
- L2：仅在触发条件满足时加载"条件必读"文件

路径约定：
- `references/...` 相对当前 skill 目录
- `../../references/...` 指向全局共享参考

## References 清单

### 根目录

- `references/analysis-template.md`：PLAN.md 模板，Step 7 必读
- `references/tech-stack-detection.md`：技术栈识别规则，Step 2 必读
- `references/difficulty-mining.md`：技术难点挖掘方法，Step 5 必读

### 全局参考

- `../../references/architecture-patterns.md`：架构模式识别库，Step 3 必读
- `../../references/diagram-patterns.md`：Mermaid 图表模式库，Step 6 必读
- `../../references/language-patterns/universal-language-detection.md`：通用语言识别，按识别语言加载

## 工具策略

- `Read/Grep`：读取项目文件、配置文件、源代码
- `Write/Edit`：生成分析报告和图表文件
- `Bash`：执行项目扫描命令
- `Task`：调用 analysis-agent、diagram-agent

## 交互流程

### Step 0：预检与上下文加载

必须做：
- 确认目标项目目录可读
- 解析项目根目录
- 加载最小参考：`references/tech-stack-detection.md`

输出：
- "已就绪输入"与"缺失输入"清单

### Step 1：项目扫描

扫描内容：
- 目录结构
- 文件类型分布
- 配置文件位置

输出：
- 文件清单（按类型分类）
- 目录结构树

### Step 2：技术栈识别

识别内容：
- 编程语言（从文件扩展名、配置文件）
- 框架（从依赖文件、代码特征）
- 构建工具（从配置文件）
- 依赖库（从 package.json、requirements.txt 等）

加载参考：
- `references/tech-stack-detection.md`
- `../../references/language-patterns/universal-language-detection.md`

输出：
- `analysis/tech-stack.json`

### Step 3：架构分析

分析内容：
- 架构模式（MVC、Layered、Microservice 等）
- 模块划分
- 入口点识别

加载参考：
- `../../references/architecture-patterns.md`

输出：
- 架构模式描述
- 模块划分清单

### Step 4：功能模块分析

分析内容：
- 各模块功能职责
- 关键文件识别
- 模块间关系

输出：
- `analysis/modules.md`

### Step 5：技术难点挖掘

挖掘内容：
- 技术难点（复杂实现、特殊处理）
- 技术亮点（创新方案、最佳实践）
- 潜在问题（技术债务、安全风险）

加载参考：
- `references/difficulty-mining.md`

输出：
- `analysis/difficulties.json`

### Step 6：图表生成

**调用 diagram-agent**，生成以下图表：

| 图表类型 | 文件名 | 说明 |
|---------|--------|------|
| 系统架构图 | `diagrams/system-architecture.md` | 展示系统整体架构 |
| 模块依赖图 | `diagrams/module-dependency.md` | 展示模块间依赖 |
| 数据流图 | `diagrams/data-flow.md` | 展示核心数据流转 |

加载参考：
- `../../references/diagram-patterns.md`

输出：
- `analysis/diagrams/*.md`

### Step 7：生成 PLAN.md

汇总所有分析结果，生成主产物 PLAN.md。

加载参考：
- `references/analysis-template.md`

PLAN.md 结构：
```markdown
# 项目技术分析报告

## 项目概览
- 项目名称
- 技术栈
- 代码规模

## 技术架构
### 架构模式
[引用 system-architecture.md 图表]

### 模块划分
[引用 module-dependency.md 图表]

## 目录组织
### 目录结构
### 职责划分

## 功能分析
### 核心功能
### 模块功能

## 数据流
[引用 data-flow.md 图表]

## 技术难点
### 难点1
### 难点2
### 难点3

## 改进建议
```

### Step 8：生成摘要

输出：
- `analysis/summary.md`
- `analysis/.analysis-state.json`

## 输出格式规范

### tech-stack.json

```json
{
  "languages": ["Python", "TypeScript"],
  "frameworks": ["FastAPI", "React"],
  "build_tools": ["npm", "pip"],
  "dependencies": {
    "production": [...],
    "development": [...]
  },
  "code_metrics": {
    "total_files": 150,
    "total_lines": 25000,
    "by_language": {...}
  }
}
```

### difficulties.json

```json
{
  "difficulties": [
    {
      "id": "diff-001",
      "title": "分布式事务处理",
      "description": "使用 Saga 模式处理跨服务事务",
      "location": "src/services/order.py",
      "difficulty_level": "high",
      "blog_potential": "high",
      "tags": ["distributed", "transaction", "saga"]
    }
  ],
  "highlights": [...],
  "potential_issues": [...]
}
```

## 质量标准

- [ ] PLAN.md 结构完整
- [ ] 至少生成3个 Mermaid 图表
- [ ] 技术栈识别准确
- [ ] 技术难点有具体代码位置
- [ ] 图表可正确渲染
- [ ] 分析结果可被 `/blog` 直接消费