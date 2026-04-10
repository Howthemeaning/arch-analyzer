# Arch Analyzer 架构详解

## 整体架构

Arch Analyzer 采用 Skill + Agent 的架构模式，通过三个核心 Skill 和三个 Agent 协同工作，实现项目分析、架构图生成和技术博客写作。

```mermaid
graph TB
    subgraph Claude Code
        subgraph Skills
            A[/init]
            B[/analysis]
            C[/blog]
        end
        
        subgraph Agents
            D[analysis-agent]
            E[diagram-agent]
            F[blog-writer-agent]
        end
        
        subgraph References
            G[通用语言识别]
            H[架构模式库]
            I[图表模式库]
            J[输出模板]
        end
    end
    
    subgraph 输出产物
        K[AGENTS.md]
        L[.roo/rules-*/AGENTS.md]
        M[analysis/]
        N[blogs/]
    end
    
    A --> D
    B --> D
    B --> E
    C --> F
    
    D --> G
    D --> H
    E --> I
    D --> J
    F --> J
    
    A --> K
    A --> L
    B --> M
    C --> N
    
    B -->|分析结果含图表| C
```

## 核心组件

### Skills

Skills 是用户可直接调用的命令，定义了执行流程和输出规范。

#### /init Skill

**职责**：分析代码库并生成 AGENTS.md 文件

**执行流程**：
1. 检查现有 AGENTS.md 等规则文件
2. 项目识别（语言、框架、构建系统）
3. 命令提取（仅非标准命令）
4. 架构映射（核心组件、入口点）
5. 模式分析（项目特有工具函数）
6. 代码风格提取（从配置文件）
7. 测试发现
8. 生成主 AGENTS.md
9. 生成模式特定文件

**核心理念**：只记录非显而易见的项目特定信息

#### /analysis Skill

**职责**：深度分析项目代码，生成 PLAN.md 和 Mermaid 图表

**执行流程**：
1. 预检与上下文加载
2. 项目扫描
3. 技术栈识别
4. 架构分析
5. 功能模块分析
6. 技术难点挖掘
7. 图表生成（调用 diagram-agent）
8. 生成 PLAN.md
9. 生成摘要

**输出产物**：
- `PLAN.md`：技术分析文档
- `analysis/tech-stack.json`：技术栈信息
- `analysis/diagrams/`：Mermaid 图表
- `analysis/modules.md`：功能模块分析
- `analysis/difficulties.json`：技术难点清单

#### /blog Skill

**职责**：基于分析结果生成技术博客

**执行流程**：
1. 预检（检查分析产物存在）
2. 加载分析结果和图表
3. 选题筛选
4. 大纲生成
5. 内容撰写
6. 自我审查
7. 修订内容（若审查不通过）
8. 保存博客

**审查标准**：总分 >= 85 通过

### Agents

Agents 是被 Skills 调用的子任务执行者，负责特定领域的分析工作。

#### analysis-agent

**职责**：项目分析 Agent，负责代码分析、技术栈识别、架构分析

**工具权限**：Read, Grep, Bash

**分析维度**：
- 技术栈：语言、框架、依赖
- 架构：模式、分层、入口
- 模块：功能、职责、关系
- 难点：复杂度、风险、亮点

#### diagram-agent

**职责**：图表生成 Agent，负责生成 Mermaid 图表

**工具权限**：Read, Write

**图表类型**：
- 系统架构图（graph TB）
- 模块依赖图（graph LR）
- 数据流图（sequenceDiagram）

#### blog-writer-agent

**职责**：博客写作 Agent，负责撰写技术博客

**工具权限**：Read, Write, Edit

**写作流程**：
- 加载分析结果
- 提取选题内容
- 生成大纲
- 撰写内容
- 自我审查

### References

References 是参考文档库，为 Skills 和 Agents 提供分析规则和模板。

#### 通用语言识别文档

**路径**：`references/language-patterns/universal-language-detection.md`

**内容**：
- 文件扩展名识别规则
- 配置文件识别规则
- 框架特征识别规则
- 通用项目结构模式

**特点**：支持所有主流编程语言，无需为每种语言单独创建模式文件。

#### 架构模式库

**路径**：`references/architecture-patterns.md`

**内容**：
- MVC、Layered、Microservice 等架构模式识别特征
- 架构模式映射表
- 混合架构识别方法

#### 图表模式库

**路径**：`references/diagram-patterns.md`

**内容**：
- 各类 Mermaid 图表模板
- 图表生成规则
- 图表最佳实践

## 数据流

```mermaid
sequenceDiagram
    participant User
    participant /init
    participant /analysis
    participant analysis-agent
    participant diagram-agent
    participant /blog
    participant blog-writer-agent
    
    User->>/init: 初始化项目
    /init->>analysis-agent: 扫描项目
    analysis-agent->>analysis-agent: 识别技术栈
    analysis-agent->>analysis-agent: 提取构建命令
    analysis-agent->>analysis-agent: 分析代码风格
    analysis-agent->>/init: 返回分析数据
    /init->>/init: 生成 AGENTS.md
    /init->>/init: 生成 .roo/rules-*/AGENTS.md
    
    User->>/analysis: 深度分析
    /analysis->>analysis-agent: 启动深度分析
    analysis-agent->>analysis-agent: 扫描项目目录
    analysis-agent->>analysis-agent: 识别技术栈
    analysis-agent->>analysis-agent: 分析架构模式
    analysis-agent->>analysis-agent: 分析功能模块
    analysis-agent->>analysis-agent: 挖掘技术难点
    /analysis->>diagram-agent: 生成架构图
    diagram-agent->>diagram-agent: 架构图
    diagram-agent->>diagram-agent: 模块依赖图
    diagram-agent->>diagram-agent: 数据流图
    /analysis->>analysis/: 保存分析报告 + 图表
    
    User->>/blog: 生成博客
    /blog->>/analysis: 读取分析报告和图表
    /blog->>blog-writer-agent: 启动写作任务
    blog-writer-agent->>blog-writer-agent: 选择技术难点选题
    blog-writer-agent->>blog-writer-agent: 引用架构图
    blog-writer-agent->>blog-writer-agent: 撰写博客内容
    blog-writer-agent->>blog-writer-agent: 自我审查
    /blog->>blogs/: 保存博客文章
```

## 命令间依赖

```mermaid
graph LR
    INIT[/init] -->|AGENTS.md| ANALYSIS[/analysis]
    ANALYSIS -->|analysis/ 目录| BLOG[/blog]
    ANALYSIS -->|diagrams/ 图表| BLOG
    
    style INIT fill:#4CAF50,color:#fff
    style ANALYSIS fill:#2196F3,color:#fff
    style BLOG fill:#FF9800,color:#fff
```

**关键约束**：
- `/blog` 依赖 `/analysis` 的输出，必须先执行 `/analysis`
- `/init` 是可选的，但建议在首次使用时执行
- `/analysis` 生成的图表可以被 `/blog` 直接引用

## 输出位置设计

**核心概念**：所有输出产物都生成在被分析的目标项目目录下，而非 arch-analyzer 插件自身目录。

这与参考项目 webnovel-writer 的模式一致：插件提供能力，产物写入用户项目。

```text
# 用户在某个项目目录下使用 arch-analyzer
cd /Users/dev/my-project        # 被分析的目标项目
claude                          # 启动 Claude Code

# 执行命令后，产物生成在目标项目目录下：
my-project/
├── AGENTS.md                   # /init 生成
├── .roo/rules-*/AGENTS.md      # /init 生成
├── PLAN.md                     # /analysis 生成
├── analysis/                   # /analysis 生成
│   ├── diagrams/               # Mermaid 图表
│   ├── tech-stack.json
│   ├── modules.md
│   └── difficulties.json
└── blogs/                      # /blog 生成
    └── YYYY-MM-DD-topic.md
```

## References 加载策略

采用分级加载策略，避免一次性加载所有参考文档：

| 等级 | 说明 | 加载时机 |
|------|------|---------|
| L0 | 不加载任何参考 | 未进入对应步骤前 |
| L1 | 仅加载该步"必读"文件 | 进入对应步骤时 |
| L2 | 加载"条件必读"文件 | 触发条件满足时 |

**路径约定**：
- `references/...`：相对当前 skill 目录
- `../../references/...`：指向全局共享参考

## 扩展性设计

### 新增语言支持

只需在 `universal-language-detection.md` 中添加识别规则，无需创建新文件。

### 新增架构模式

在 `architecture-patterns.md` 中添加新的架构模式识别特征。

### 新增图表类型

在 `diagram-patterns.md` 中添加新的图表模板。

### 新增 Skill

1. 创建 `arch-analyzer/skills/new-skill/SKILL.md`
2. 在 `plugin.json` 中注册
3. 创建必要的 references 文件