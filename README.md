# Arch Analyzer

[![License](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)
[![Claude Code Compatible](https://img.shields.io/badge/Claude%20Code-Compatible-green.svg)](https://claude.ai)

## 项目简介

`Arch Analyzer` 是基于 Claude Code 的项目分析套件，帮助开发者快速理解项目架构、发现技术难点，并生成可发布的技术博客。

## 核心功能

- `/init`：生成 AGENTS.md，让 AI 助手立即高效工作
- `/analysis`：深度分析项目，生成 PLAN.md 和 Mermaid 架构图
- `/blog`：基于分析结果生成技术博客，自动引用图表

## 特性

- **通用语言支持**：支持所有主流编程语言（Python、JavaScript/TypeScript、Java、Go、Rust、Ruby、PHP、C/C++、C#、Swift 等）
- **多 Agent 协作**：分析 Agent、博客写作 Agent、图表生成 Agent 协同工作
- **可视化架构图**：自动生成 Mermaid 架构图、模块依赖图、数据流图
- **结构化输出**：生成标准化的 AGENTS.md、技术分析文档和博客文章

## 快速开始

### 1. 安装插件

```bash
claude plugin marketplace add Howthemeaning/arch-analyzer --scope user
```

### 2. 在目标项目中使用

```bash
cd /path/to/your-project
claude

# 在 Claude Code 中执行
/init        # 生成 AGENTS.md
/analysis    # 生成 PLAN.md 和架构图
/blog        # 生成技术博客
```

### 3. 输出产物

所有产物生成在目标项目目录下：

```text
your-project/
├── AGENTS.md              # AI 助手引导文件
├── PLAN.md                # 技术分析文档
├── analysis/
│   ├── tech-stack.json    # 技术栈信息
│   ├── diagrams/          # Mermaid 图表
│   │   ├── system-architecture.md
│   │   ├── module-dependency.md
│   │   └── data-flow.md
│   ├── modules.md         # 功能模块分析
│   └── difficulties.json  # 技术难点清单
└── blogs/
    └── YYYY-MM-DD-topic.md  # 技术博客
```

## 命令详解

### /init

分析代码库并生成 AGENTS.md 文件，让 AI 助手能立即高效地工作。

**核心理念**：只记录**非显而易见**的项目特定信息，排除所有标准实践和框架默认值。

**输出**：
- `AGENTS.md`：主引导文件（约20行）
- `.roo/rules-code/AGENTS.md`：编码模式特定规则
- `.roo/rules-debug/AGENTS.md`：调试模式特定规则
- `.roo/rules-ask/AGENTS.md`：问答模式特定规则
- `.roo/rules-architect/AGENTS.md`：架构模式特定规则

### /analysis

深度分析项目代码，生成技术分析文档 PLAN.md 和 Mermaid 架构图。

**分析内容**：
- 技术栈识别（语言、框架、依赖）
- 架构模式分析（MVC、分层、微服务等）
- 功能模块分析
- 技术难点挖掘

**输出**：
- `PLAN.md`：技术分析文档
- `analysis/tech-stack.json`：技术栈信息
- `analysis/diagrams/`：Mermaid 图表目录
- `analysis/modules.md`：功能模块分析
- `analysis/difficulties.json`：技术难点清单

### /blog

基于分析结果生成可发布的技术博客，自动引用 Mermaid 图表。

**流程**：
1. 加载分析结果和图表
2. 筛选适合博客的选题
3. 生成大纲和内容
4. 自我审查（评分 >= 85 通过）
5. 保存博客文件

**输出**：
- `blogs/YYYY-MM-DD-topic-slug.md`：技术博客

## 详细文档

- [架构设计](docs/architecture.md)
- [命令详解](docs/commands.md)

## 项目结构

```text
arch-analyzer/
├── README.md                          # 项目主文档
├── plugin.json                        # Claude Code 插件配置
├── marketplace.json                   # Marketplace 发布配置
├── LICENSE                            # 开源协议
│
├── docs/                              # 文档目录
│   ├── architecture.md                # 架构详解
│   ├── commands.md                    # 命令说明
│   └── README.md                      # 文档导航
│
├── arch-analyzer/                     # 插件核心目录
│   ├── agents/                        # Agent 定义
│   │   ├── analysis-agent.md          # 项目分析 Agent
│   │   ├── diagram-agent.md           # 图表生成 Agent
│   │   └── blog-writer-agent.md       # 博客写作 Agent
│   │
│   ├── skills/                        # Skill 定义
│   │   ├── init/                      # /init 命令
│   │   │   ├── SKILL.md               # Skill 主文件
│   │   │   └── references/            # 参考文档
│   │   │       └── agents-md-template.md
│   │   │
│   │   ├── analysis/                  # /analysis 命令
│   │   │   ├── SKILL.md               # Skill 主文件
│   │   │   └── references/            # 参考文档
│   │   │       ├── analysis-template.md
│   │   │       ├── tech-stack-detection.md
│   │   │       └── difficulty-mining.md
│   │   │
│   │   └── blog/                      # /blog 命令
│   │       ├── SKILL.md               # Skill 主文件
│   │       └── references/            # 参考文档
│   │           ├── blog-template.md
│   │           ├── writing-style.md
│   │           └── review-checklist.md
│   │
│   └── references/                    # 全局参考文档
│       ├── language-patterns/         # 语言特定模式
│       │   └── universal-language-detection.md
│       ├── architecture-patterns.md   # 架构模式库
│       └── diagram-patterns.md        # Mermaid 图表模式库
```

## 开源协议

MIT License

## 作者

Howthemeaning - https://github.com/Howthemeaning