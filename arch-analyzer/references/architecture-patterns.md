# 架构模式识别库

## 常见架构模式

### MVC (Model-View-Controller)

**识别特征**：
- `controllers/` 目录
- `models/` 目录
- `views/` 目录
- 路由配置文件

**常见框架**：
- Ruby on Rails
- Django (MTV 变体)
- Spring MVC
- ASP.NET MVC

### Layered Architecture (分层架构)

**识别特征**：
- `api/` 或 `controller/` 层
- `service/` 或 `business/` 层
- `repository/` 或 `dao/` 层
- `model/` 或 `entity/` 层

**常见变体**：
- 三层架构
- 四层架构
- N层架构

### Microservice (微服务)

**识别特征**：
- 多个独立服务目录
- `docker-compose.yml`
- 服务间通信配置
- 独立数据库配置
- API Gateway 配置

**常见模式**：
- API Gateway
- Service Discovery
- Event-driven
- Saga 模式

### Clean Architecture

**识别特征**：
- `entities/` 目录
- `usecases/` 或 `application/` 目录
- `interfaces/` 或 `adapters/` 目录
- `infrastructure/` 或 `frameworks/` 目录

**核心原则**：
- 依赖向内
- 业务逻辑独立
- 外部框架隔离

### DDD (Domain-Driven Design)

**识别特征**：
- `domain/` 目录
- `application/` 目录
- `infrastructure/` 目录
- `interfaces/` 目录
- 聚合、实体、值对象模式

**核心概念**：
- Bounded Context
- Aggregate
- Domain Event
- Repository Pattern

### Monorepo

**识别特征**：
- `packages/` 目录
- `apps/` 目录
- workspace 配置
- 共享依赖

**常见工具**：
- npm workspaces
- yarn workspaces
- lerna
- turborepo
- nx

### Hexagonal Architecture (六边形架构)

**识别特征**：
- `core/` 或 `domain/` 目录
- `ports/` 目录
- `adapters/` 目录

**核心原则**：
- 业务逻辑在核心
- 外部依赖通过端口和适配器

### Event-Driven Architecture

**识别特征**：
- `events/` 目录
- `handlers/` 或 `listeners/` 目录
- 消息队列配置
- 事件总线实现

**常见模式**：
- Event Sourcing
- CQRS
- Pub/Sub

## 架构模式映射表

| 目录特征 | 可能的架构模式 |
|---------|---------------|
| controllers/models/views | MVC |
| api/service/repository | Layered |
| entities/usecases/interfaces | Clean Architecture |
| domain/application/infrastructure | DDD |
| packages/apps | Monorepo |
| 多服务 + docker-compose | Microservice |
| core/ports/adapters | Hexagonal |
| events/handlers | Event-Driven |

## 混合架构识别

现代项目常采用混合架构，识别时需注意：

1. **优先识别主导模式**：根据目录结构的主要特征
2. **识别子模式**：某些模块可能采用不同架构
3. **识别演进趋势**：项目可能正在从一种架构迁移到另一种

## 架构模式分析要点

### 入口点识别

- Web 应用：`main.py`、`app.py`、`index.js`、`server.js`
- CLI 应用：`cli.py`、`cli.js`、`main.rs`
- 库：`__init__.py`、`index.ts`、`lib.rs`
- 微服务：各服务的入口文件

### 模块边界识别

- 目录分隔
- 包/模块定义
- 接口文件
- 依赖关系

### 数据流识别

- API 入口 → 业务处理 → 数据存储
- 事件触发 → 处理器 → 状态变更
- 用户交互 → 状态更新 → UI 渲染