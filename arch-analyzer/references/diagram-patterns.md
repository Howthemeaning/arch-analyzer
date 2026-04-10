# Mermaid 图表模式库

## 系统架构图 (graph TB)

### 基本模板

```mermaid
graph TB
    subgraph 客户端
        A[Web App]
        B[Mobile App]
    end
    
    subgraph 服务端
        C[API Gateway]
        D[Service A]
        E[Service B]
    end
    
    subgraph 数据层
        F[Database]
        G[Cache]
    end
    
    A --> C
    B --> C
    C --> D
    C --> E
    D --> F
    E --> F
    D --> G
```

### 命名规则

- 节点使用组件名称，避免引号
- 使用 subgraph 组织相关组件
- 箭头方向：调用/依赖方向

### 分层架构模板

```mermaid
graph TB
    subgraph Presentation
        A[UI Components]
        B[Controllers]
    end
    
    subgraph Business
        C[Services]
        D[Domain Logic]
    end
    
    subgraph Data
        E[Repositories]
        F[Database]
    end
    
    A --> B
    B --> C
    C --> D
    D --> E
    E --> F
```

## 模块依赖图 (graph LR)

### 基本模板

```mermaid
graph LR
    A[模块A] --> B[模块B]
    A --> C[模块C]
    B --> D[模块D]
    C --> D
```

### 依赖类型

- `-->`：直接依赖
- `-.->`：间接依赖
- `==>`：强依赖

### Monorepo 模板

```mermaid
graph LR
    subgraph Apps
        A[Web App]
        B[Mobile App]
    end
    
    subgraph Packages
        C[Core]
        D[UI]
        E[Utils]
    end
    
    A --> C
    A --> D
    B --> C
    B --> D
    C --> E
    D --> E
```

## 数据流图 (sequenceDiagram)

### 基本模板

```mermaid
sequenceDiagram
    participant U as 用户
    participant F as 前端
    participant A as API
    participant S as Service
    participant D as Database
    
    U->>F: 发起请求
    F->>A: HTTP请求
    A->>S: 业务调用
    S->>D: 数据操作
    D-->>S: 返回数据
    S-->>A: 业务结果
    A-->>F: HTTP响应
    F-->>U: 显示结果
```

### 常用语法

- `->>`：同步请求
- `-->>`：异步响应
- `->>+`：激活
- `-->>-`：deactivate
- `--x`：失败

### 认证流程模板

```mermaid
sequenceDiagram
    participant U as 用户
    participant F as 前端
    participant A as Auth Service
    participant D as Database
    
    U->>F: 输入凭证
    F->>A: 发送认证请求
    A->>D: 查询用户
    D-->>A: 用户数据
    A->>A: 验证凭证
    A->>A: 生成Token
    A-->>F: 返回Token
    F->>F: 存储Token
    F-->>U: 登录成功
```

## 类图 (classDiagram)

### 基本模板

```mermaid
classDiagram
    class User {
        +String name
        +String email
        +login()
        +logout()
    }
    
    class AuthService {
        +authenticate()
        +validateToken()
    }
    
    User --> AuthService
```

### 关系类型

- `-->`：关联
- `-->`：继承
- `--*`：组合
- `--o`：聚合
- `--|>`：实现

### DDD 模板

```mermaid
classDiagram
    class Order {
        +OrderId id
        +List~OrderItem~ items
        +addItem()
        +submit()
    }
    
    class OrderItem {
        +ProductId productId
        +int quantity
        +Money price
    }
    
    class Product {
        +ProductId id
        +String name
        +Money price
    }
    
    Order *-- OrderItem
    OrderItem --> Product
```

## 状态图 (stateDiagram-v2)

### 基本模板

```mermaid
stateDiagram-v2
    [*] --> 待处理
    待处理 --> 处理中
    处理中 --> 已完成
    处理中 --> 失败
    已完成 --> [*]
    失败 --> [*]
```

### 订单状态模板

```mermaid
stateDiagram-v2
    [*] --> Created
    Created --> Pending: 提交
    Pending --> Paid: 支付
    Pending --> Cancelled: 取消
    Paid --> Shipped: 发货
    Shipped --> Delivered: 送达
    Delivered --> [*]
    Cancelled --> [*]
```

## 流程图 (flowchart)

### 基本模板

```mermaid
flowchart TD
    A[开始] --> B{条件判断}
    B -->|是| C[处理A]
    B -->|否| D[处理B]
    C --> E[结束]
    D --> E
```

### 决策流程模板

```mermaid
flowchart TD
    A[接收请求] --> B{验证权限}
    B -->|有权限| C{数据校验}
    B -->|无权限| D[拒绝访问]
    C -->|有效| E[处理业务]
    C -->|无效| F[返回错误]
    E --> G[返回结果]
    D --> G
    F --> G
```

## 图表最佳实践

1. **简洁**：避免过多节点，保持可读性
2. **命名**：使用清晰的中文名称
3. **分组**：使用 subgraph 组织相关内容
4. **方向**：从上到下或从左到右
5. **注释**：在图表外添加说明文字
6. **一致性**：同一项目中图表风格保持一致

## 图表选择指南

| 分析内容 | 推荐图表类型 |
|---------|-------------|
| 系统整体结构 | graph TB |
| 模块依赖关系 | graph LR |
| 数据流转过程 | sequenceDiagram |
| 类/对象关系 | classDiagram |
| 状态变化 | stateDiagram-v2 |
| 业务流程 | flowchart |