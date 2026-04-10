# Arch Analyzer 文档导航

## 快速链接

- [README.md](../README.md) - 项目主文档
- [架构详解](architecture.md) - 架构设计说明
- [命令详解](commands.md) - 命令使用说明

## 文档目录

### 用户文档

| 文档 | 说明 |
|------|------|
| [README.md](../README.md) | 项目简介、快速开始、核心功能 |
| [commands.md](commands.md) | `/init`、`/analysis`、`/blog` 命令详解 |

### 架构文档

| 文档 | 说明 |
|------|------|
| [architecture.md](architecture.md) | 整体架构、核心组件、数据流 |

### 开发文档

| 文档 | 说明 |
|------|------|
| [plans/architecture-design.md](../plans/architecture-design.md) | 架构设计文档（开发用） |
| [plans/implementation-spec.md](../plans/implementation-spec.md) | 实现规范文档（开发用） |

## 核心概念

### Skills

Skills 是用户可直接调用的命令：

- **[/init](commands.md#init)**：生成 AGENTS.md
- **[/analysis](commands.md#analysis)**：深度分析项目
- **[/blog](commands.md#blog)**：生成技术博客

### Agents

Agents 是被 Skills 调用的子任务执行者：

- **analysis-agent**：项目分析 Agent
- **diagram-agent**：图表生成 Agent
- **blog-writer-agent**：博客写作 Agent

### References

References 是参考文档库：

- **通用语言识别**：支持所有主流编程语言
- **架构模式库**：MVC、分层、微服务等架构识别
- **图表模式库**：Mermaid 图表模板

## 输出位置

**所有输出产物都生成在被分析的目标项目目录下**：

```text
target-project/
├── AGENTS.md              # /init 生成
├── .roo/rules-*/AGENTS.md # /init 生成
├── PLAN.md                # /analysis 生成
├── analysis/              # /analysis 生成
│   ├── tech-stack.json
│   ├── diagrams/
│   ├── modules.md
│   └── difficulties.json
└── blogs/                 # /blog 生成
    └── YYYY-MM-DD-topic.md
```

## 使用流程

```mermaid
flowchart LR
    A[/init] --> B[/analysis]
    B --> C[/blog]
    
    style A fill:#4CAF50,color:#fff
    style B fill:#2196F3,color:#fff
    style C fill:#FF9800,color:#fff
```

1. **首次使用**：执行 `/init` 生成 AGENTS.md
2. **分析项目**：执行 `/analysis` 生成分析报告和图表
3. **生成博客**：执行 `/blog` 基于分析结果生成技术博客

## 支持的语言

Arch Analyzer 支持所有主流编程语言：

- Python
- JavaScript / TypeScript
- Java / Kotlin
- Go
- Rust
- Ruby
- PHP
- C / C++
- C#
- Swift
- Scala
- Elixir
- Haskell
- 以及更多...

详见 [通用语言识别文档](../arch-analyzer/references/language-patterns/universal-language-detection.md)。