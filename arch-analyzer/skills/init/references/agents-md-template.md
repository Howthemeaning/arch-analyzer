# AGENTS.md 模板

## 文件头部（必须）

```markdown
# AGENTS.md

This file provides guidance to agents when working with code in this repository.
```

## 内容结构（按需填充）

### Build Commands（仅非标准）

```markdown
## Build Commands
- [非标准命令说明]
- [特殊目录要求]
```

**示例**：
```markdown
## Build Commands
- Run tests from `packages/core/` directory, not root (vitest config location)
- `npm run dev:all` starts all services (not just `npm run dev`)
```

### Code Style（仅项目特定）

```markdown
## Code Style
- [项目特定规则，未被 linter 强制]
- [自定义工具函数引用]
```

**示例**：
```markdown
## Code Style
- Use `safeWriteJson()` from `src/utils/file.ts` for JSON writes (prevents corruption)
- API calls must use retry wrapper in `src/api/utils/retry.ts`
```

### Architecture（仅非显而易见）

```markdown
## Architecture
- [非标准目录结构说明]
- [隐藏依赖说明]
```

**示例**：
```markdown
## Architecture
- `src/` is VSCode extension, not web app source (counterintuitive)
- Webview and extension communicate via IPC in `packages/ipc/src/`
```

### Testing（仅非标准）

```markdown
## Testing
- [非标准测试配置]
- [特殊测试要求]
```

**示例**：
```markdown
## Testing
- Test files must be in same directory as source for vitest to work
- Integration tests require `docker-compose up` first
```

## 排除内容（不要写）

以下内容**不要**写入 AGENTS.md：

- 标准 npm/pip 命令（如 `npm install`、`npm test`）
- 框架默认配置（如 Next.js 的 `pages/` 目录）
- 常见目录结构（如 `src/`、`tests/`）
- 可从配置文件读取的信息（如 ESLint 规则）
- 通用编程实践（如 "使用驼峰命名"）
- 框架标准用法（如 React 组件写法）

## 质量检查清单

- [ ] 每行都是非显而易见信息
- [ ] 无标准实践、框架默认值
- [ ] 文件尽可能短（约20行）
- [ ] 包含具体文件路径
- [ ] 更新时文件变短而非变长

## 测试标准

**问自己**：经验丰富的开发者阅读此文件后，会感到惊讶吗？

- 如果答案是"不会"，说明内容太明显，应该删除
- 如果答案是"会"，说明内容有价值，应该保留

## 模式特定文件模板

### .roo/rules-code/AGENTS.md

```markdown
# Project Coding Rules (Non-Obvious Only)

- [自定义工具函数使用规则]
- [隐藏依赖说明]
- [必须遵循的非标准模式]
```

### .roo/rules-debug/AGENTS.md

```markdown
# Project Debugging Rules (Non-Obvious Only)

- [非标准调试工具]
- [隐藏日志位置]
- [导致静默失败的陷阱]
```

### .roo/rules-ask/AGENTS.md

```markdown
# Project Documentation Context (Non-Obvious Only)

- [隐藏或误导性的文档位置]
- [与文件结构不符的实际组织]
```

### .roo/rules-architect/AGENTS.md

```markdown
# Project Architecture Constraints (Non-Obvious Only)

- [隐藏耦合说明]
- [未文档化的架构决策]
- [必须遵循的非标准模式]