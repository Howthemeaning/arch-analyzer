---
name: arch-init
description: 分析代码库并生成 AGENTS.md 文件，让 AI 助手能立即高效地工作。只记录非显而易见的项目特定信息。
allowed-tools: Read, Grep, Write, Edit, Bash, Task, AskUserQuestion
---

# Project Initialization (AGENTS.md Generator)

## 目标

- 分析代码库，提取项目特定的非显而易见信息
- 生成精简的 AGENTS.md 文件（约20行，复杂项目可扩展）
- 生成 .roo/rules-*/AGENTS.md 模式特定文件
- 让 AI 助手能立即高效地工作，避免常见错误

## 执行原则

1. **非显而易见原则**：只记录必须通过阅读文件才能发现的信息
2. **排除标准实践**：不记录框架默认值、常见模式、标准命令
3. **精简优先**：文件应尽可能短，每行都必须有价值
4. **更新时缩短**：更新现有文件时，先删除明显信息，文件应变短而非变长

## 输出位置

**所有产物生成在被分析的目标项目目录下**：

```text
target-project/
├── AGENTS.md                   # 主引导文件
└── .roo/
    ├── rules-code/AGENTS.md    # 编码模式特定规则
    ├── rules-debug/AGENTS.md   # 调试模式特定规则
    ├── rules-ask/AGENTS.md     # 问答模式特定规则
    └── rules-architect/AGENTS.md # 架构模式特定规则
```

## References 加载等级

- L0：未确认任务前，不预加载参考
- L1：启动时加载 `references/agents-md-template.md`
- L2：按需加载语言模式（识别到特定语言时）

路径约定：
- `references/...` 相对当前 skill 目录

## 工具策略

- `Read/Grep`：读取项目文件、配置文件、现有 AGENTS.md
- `Write/Edit`：生成或更新 AGENTS.md 文件
- `Bash`：执行项目扫描命令
- `Task`：并行分析子任务
- `AskUserQuestion`：关键分歧裁决

## 交互流程

### Step 0：检查现有文件

检查以下路径（相对目标项目根目录）：
- `AGENTS.md`
- `.roo/rules-code/AGENTS.md`
- `.roo/rules-debug/AGENTS.md`
- `.roo/rules-ask/AGENTS.md`
- `.roo/rules-architect/AGENTS.md`
- `CLAUDE.md`
- `.cursorrules`
- `.cursor/rules/`
- `.github/copilot-instructions.md`

若已存在：
- **先删除所有明显信息**
- 移除标准实践、框架默认值
- 只保留真正非显而易见的项目特定信息
- 文件应变短而非变长

### Step 1：项目识别

识别内容：
- 语言、框架、构建系统
- 包管理器和依赖文件
- 项目类型（库/应用/CLI/Monorepo）

检查文件：
- `package.json`、`requirements.txt`、`go.mod`、`Cargo.toml`
- `pom.xml`、`build.gradle`
- 目录结构特征

### Step 2：命令提取

**只提取非标准命令**：
- 与 package.json scripts 不同的命令
- 特定目录下才能运行的命令
- 需要特殊环境变量的命令

**排除**：
- 标准的 `npm test`、`npm run build`（除非有特殊要求）
- 框架默认命令

### Step 3：架构映射

识别内容：
- 核心组件和入口点
- 非标准的目录结构
- 模块间隐藏依赖

### Step 4：模式分析

发现内容：
- 项目特有的工具函数（需读取代码发现）
- 非标准模式（与典型实践不同）
- 自定义约定（未被 linter 强制）

### Step 5：代码风格提取

**只从配置文件提取**：
- `.eslintrc`、`.prettierrc`、`pyproject.toml`
- `checkstyle.xml`、`rustfmt.toml`

**排除**：
- 可从配置文件直接读取的信息
- 标准风格约定

### Step 6：测试发现

识别内容：
- 测试框架和运行方式
- 非标准的测试目录要求
- 特殊的测试配置

### Step 7：生成主 AGENTS.md

文件头部：
```markdown
# AGENTS.md

This file provides guidance to agents when working with code in this repository.
```

内容要求：
- 每行都必须是"非显而易见"的信息
- 排除所有标准实践、框架默认值、常见模式
- 约20行，复杂项目可扩展
- 包含具体文件路径引用

### Step 8：生成模式特定文件

`.roo/rules-code/AGENTS.md`：
- 编码相关的非显而易见规则
- 自定义工具函数、隐藏依赖
- 必须遵循的非标准模式

`.roo/rules-debug/AGENTS.md`：
- 调试相关的非显而易见信息
- 非标准调试工具、隐藏日志位置
- 导致静默失败的陷阱

`.roo/rules-ask/AGENTS.md`：
- 文档相关的非显而易见上下文
- 隐藏或误导性的文档位置
- 与文件结构不符的实际组织

`.roo/rules-architect/AGENTS.md`：
- 架构相关的非显而易见约束
- 隐藏耦合、未文档化的架构决策
- 必须遵循的非标准模式

## 质量标准

- [ ] 每行都是非显而易见信息
- [ ] 无标准实践、框架默认值
- [ ] 文件尽可能短
- [ ] 包含具体文件路径
- [ ] 更新时文件变短而非变长
- [ ] 测试：经验丰富的开发者会感到惊讶吗？

## 示例输出

### AGENTS.md 示例

```markdown
# AGENTS.md

This file provides guidance to agents when working with code in this repository.

## Build Commands
- Run tests from `packages/core/` directory, not root (vitest config location)
- `npm run dev:all` starts all services (not just `npm run dev`)

## Code Style
- Use `safeWriteJson()` from `src/utils/file.ts` for JSON writes (prevents corruption)
- API calls must use retry wrapper in `src/api/utils/retry.ts`

## Architecture
- `src/` is VSCode extension, not web app source (counterintuitive)
- Webview and extension communicate via IPC in `packages/ipc/src/`
```

### .roo/rules-code/AGENTS.md 示例

```markdown
# Project Coding Rules (Non-Obvious Only)

- Always use safeWriteJson() from src/utils/ instead of JSON.stringify for file writes
- API retry mechanism in src/api/providers/utils/ is mandatory
- Database queries MUST use the query builder in packages/evals/src/db/queries/
- Test files must be in same directory as source for vitest to work