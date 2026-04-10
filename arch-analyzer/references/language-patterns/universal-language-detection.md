# 通用语言识别文档

> 本文档提供通用的编程语言识别规则，支持所有主流编程语言的项目分析。

## 语言识别规则

### 通过文件扩展名识别

| 扩展名 | 语言 | 备注 |
|--------|------|------|
| .py | Python | |
| .pyw | Python | Windows GUI |
| .pyx | Python | Cython |
| .js | JavaScript | |
| .mjs | JavaScript | ES Module |
| .cjs | JavaScript | CommonJS |
| .ts | TypeScript | |
| .tsx | TypeScript | React |
| .jsx | JavaScript | React |
| .vue | Vue | |
| .svelte | Svelte | |
| .java | Java | |
| .kt | Kotlin | |
| .kts | Kotlin | Script |
| .go | Go | |
| .rs | Rust | |
| .rb | Ruby | |
| .php | PHP | |
| .c | C | |
| .h | C | Header |
| .cpp | C++ | |
| .hpp | C++ | Header |
| .cc | C++ | |
| .cxx | C++ | |
| .cs | C# | |
| .swift | Swift | |
| .m | Objective-C | |
| .mm | Objective-C++ | |
| .scala | Scala | |
| .sc | Scala | Script |
| .clj | Clojure | |
| .cljs | ClojureScript | |
| .ex | Elixir | |
| .exs | Elixir | Script |
| .erl | Erlang | |
| .hrl | Erlang | Header |
| .hs | Haskell | |
| .lhs | Haskell | Literate |
| .ml | OCaml | |
| .mli | OCaml | Interface |
| .fs | F# | |
| .fsi | F# | Interface |
| .fsx | F# | Script |
| .lua | Lua | |
| .pl | Perl | |
| .pm | Perl | Module |
| .r | R | |
| .R | R | |
| .jl | Julia | |
| .nim | Nim | |
| .cr | Crystal | |
| .d | D | |
| .di | D | Interface |
| .groovy | Groovy | |
| .gy | Groovy | |
| .gsh | Groovy | Shell |
| .dart | Dart | |
| .sql | SQL | |
| .sh | Shell | Bash |
| .bash | Shell | Bash |
| .zsh | Shell | Zsh |
| .ps1 | PowerShell | |
| .psm1 | PowerShell | Module |
| .asm | Assembly | |
| .s | Assembly | |
| .sol | Solidity | Smart Contract |
| .vy | Vyper | Smart Contract |
| .pkl | Pkl | Configuration |
| .json | JSON | Data |
| .yaml | YAML | Data |
| .yml | YAML | Data |
| .toml | TOML | Data |
| .xml | XML | Data |
| .proto | Protocol Buffers | |
| .graphql | GraphQL | |
| .gql | GraphQL | |

### 通过配置文件识别

| 配置文件 | 语言/框架 | 备注 |
|----------|----------|------|
| package.json | JavaScript/TypeScript/Node.js | npm/yarn/pnpm |
| tsconfig.json | TypeScript | |
| jsconfig.json | JavaScript | |
| .eslintrc.* | JavaScript/TypeScript | ESLint |
| .prettierrc.* | JavaScript/TypeScript | Prettier |
| requirements.txt | Python | pip |
| pyproject.toml | Python | Modern Python |
| setup.py | Python | Traditional |
| Pipfile | Python | pipenv |
| poetry.lock | Python | poetry |
| go.mod | Go | |
| go.sum | Go | |
| Cargo.toml | Rust | |
| Cargo.lock | Rust | |
| pom.xml | Java | Maven |
| build.gradle | Java | Gradle |
| build.gradle.kts | Java/Kotlin | Gradle Kotlin DSL |
| Gemfile | Ruby | Bundler |
| .gemspec | Ruby | |
| composer.json | PHP | Composer |
| CMakeLists.txt | C/C++ | CMake |
| Makefile | C/C++/Any | Make |
| *.csproj | C# | .NET |
| Package.swift | Swift | |
| Podfile | Objective-C/Swift | CocoaPods |
| Cartfile | Objective-C/Swift | Carthage |
| build.sbt | Scala | sbt |
| mix.exs | Elixir | Mix |
| rebar.config | Erlang | Rebar3 |
| stack.yaml | Haskell | Stack |
| cabal.project | Haskell | Cabal |
| Project.toml | Julia | |
| dub.sdl | D | DUB |
| dub.json | D | DUB |
| pubspec.yaml | Dart/Flutter | |
| shard.yml | Crystal | Shards |
| nimble.nimble | Nim | Nimble |
| Package.resolved | Swift | SPM |
| project.clj | Clojure | Leiningen |
| deps.edn | Clojure | CLI |
| nuget.config | C#/.NET | NuGet |
| vcpkg.json | C/C++ | vcpkg |
| conanfile.txt | C/C++ | Conan |
| conanfile.py | C/C++ | Conan |

### 通过目录结构识别

| 目录特征 | 语言/框架 |
|----------|----------|
| __pycache__/ | Python |
| node_modules/ | JavaScript/TypeScript |
| src/main/java/ | Java (Maven) |
| app/src/main/java/ | Android |
| pkg/ | Go |
| vendor/ | Go / PHP |
| target/ | Java (Maven) / Rust |
| build/ | Java (Gradle) / C/C++ |
| dist/ | JavaScript/TypeScript |
| .venv/ / venv/ | Python |
| .env/ | Python |
| Pods/ | iOS |
| Carthage/ | iOS |
| .dart_tool/ | Dart |
| .elixir_ls/ | Elixir |
| .stack-work/ | Haskell |
| .cabal-sandbox/ | Haskell |
| elm-stuff/ | Elm |
| bower_components/ | JavaScript (Legacy) |
| jspm_packages/ | JavaScript (Legacy) |

## 框架识别规则

### Web 框架

| 框架 | 识别特征 |
|------|---------|
| Django | `django` in requirements, `manage.py`, `settings.py` |
| FastAPI | `fastapi` in requirements, `app/main.py` |
| Flask | `flask` in requirements, `app.py` or `wsgi.py` |
| Express | `express` in dependencies, `app.js` or `server.js` |
| NestJS | `@nestjs/core` in dependencies, `modules/` |
| Next.js | `next` in dependencies, `pages/` or `app/` |
| Nuxt.js | `nuxt` in dependencies, `pages/` |
| React | `react` in dependencies, `components/` |
| Vue | `vue` in dependencies, `.vue` files |
| Angular | `@angular/core` in dependencies, `*.module.ts` |
| Svelte | `svelte` in dependencies, `.svelte` files |
| Spring Boot | `spring-boot` in pom.xml, `@SpringBootApplication` |
| Rails | `rails` in Gemfile, `app/controllers/` |
| Laravel | `laravel` in composer.json, `app/Http/` |
| Gin | `gin-gonic` in go.mod |
| Echo | `labstack/echo` in go.mod |
| Actix | `actix-web` in Cargo.toml |
| Rocket | `rocket` in Cargo.toml |

### 移动框架

| 框架 | 识别特征 |
|------|---------|
| React Native | `react-native` in dependencies |
| Flutter | `flutter` in pubspec.yaml |
| Ionic | `@ionic/angular` or `@ionic/react` in dependencies |
| SwiftUI | `SwiftUI` imports, `.swift` files |
| UIKit | `UIKit` imports, `.swift` or `.m` files |
| Kotlin Android | `androidx` in dependencies, `.kt` files |
| Java Android | `androidx` in dependencies, `.java` files |

### 测试框架

| 框架 | 识别特征 |
|------|---------|
| pytest | `pytest` in requirements, `test_*.py` |
| unittest | `unittest` imports, `test_*.py` |
| Jest | `jest` in dependencies, `*.test.js` or `*.spec.js` |
| Mocha | `mocha` in dependencies, `test/` |
| Vitest | `vitest` in dependencies, `*.test.ts` |
| JUnit | `junit` in pom.xml, `Test*.java` |
| TestNG | `testng` in pom.xml |
| Go test | `_test.go` files |
| Rust test | `#[test]` attributes |
| RSpec | `rspec` in Gemfile, `*_spec.rb` |
| PHPUnit | `phpunit` in composer.json |

### ORM/数据库

| 工具 | 识别特征 |
|------|---------|
| SQLAlchemy | `sqlalchemy` in requirements |
| Django ORM | `django.db.models` imports |
| Prisma | `prisma` in dependencies, `prisma/schema.prisma` |
| TypeORM | `typeorm` in dependencies |
| Sequelize | `sequelize` in dependencies |
| JPA/Hibernate | `javax.persistence` or `jakarta.persistence` |
| MyBatis | `mybatis` in pom.xml |
| Entity Framework | `EntityFrameworkCore` in *.csproj |
| GORM | `gorm` in go.mod |
| Diesel | `diesel` in Cargo.toml |

## 通用项目结构模式

### 分层架构（适用于所有语言）

| 目录 | 职责 |
|------|------|
| api/ / controllers/ / routes/ | API 层，处理请求 |
| services/ / business/ / domain/ | 业务层，核心逻辑 |
| models/ / entities/ / domain/ | 数据层，数据模型 |
| repositories/ / dao/ / data/ | 数据访问层 |
| utils/ / common/ / lib/ | 工具函数 |
| config/ / settings/ / env/ | 配置文件 |

### MVC 模式

| 目录 | 职责 |
|------|------|
| controllers/ / controller/ | 控制器，处理请求 |
| models/ / model/ | 模型，数据逻辑 |
| views/ / view/ / templates/ | 视图，展示层 |

### 微服务模式

| 目录/文件 | 说明 |
|----------|------|
| services/ / apps/ | 多个独立服务 |
| docker-compose.yml | 容器编排 |
| Dockerfile | 容器构建 |
| api-gateway/ | API 网关 |
| service-discovery/ | 服务发现 |

### Monorepo 模式

| 目录 | 说明 |
|------|------|
| packages/ / libs/ | 共享包 |
| apps/ / projects/ | 应用项目 |
| tools/ | 开发工具 |
| docs/ | 文档 |

## 构建工具识别

| 工具 | 配置文件 |
|------|----------|
| npm | package.json, package-lock.json |
| yarn | package.json, yarn.lock |
| pnpm | package.json, pnpm-lock.yaml |
| pip | requirements.txt |
| poetry | pyproject.toml, poetry.lock |
| pipenv | Pipfile, Pipfile.lock |
| Maven | pom.xml |
| Gradle | build.gradle, build.gradle.kts |
| Make | Makefile |
| CMake | CMakeLists.txt |
| Cargo | Cargo.toml, Cargo.lock |
| Go build | go.mod, go.sum |
| Bundler | Gemfile, Gemfile.lock |
| Composer | composer.json, composer.lock |
| sbt | build.sbt |
| Mix | mix.exs |
| Stack | stack.yaml |
| NuGet | *.csproj, packages.config |
| vcpkg | vcpkg.json |
| Conan | conanfile.txt, conanfile.py |

## 代码特征识别

### 通用代码模式

| 模式 | 识别特征 |
|------|---------|
| 依赖注入 | `inject`, `DI`, `Container`, `@Inject` |
| 工厂模式 | `Factory`, `create*` 方法 |
| 单例模式 | `Singleton`, `getInstance` |
| 观察者模式 | `Observer`, `Listener`, `Event`, `subscribe` |
| 策略模式 | `Strategy`, `Policy` |
| 适配器模式 | `Adapter`, `Wrapper` |
| 装饰器模式 | `Decorator`, `Wrapper` |
| 代理模式 | `Proxy` |
| 建造者模式 | `Builder` |

### 并发模式

| 模式 | 识别特征 |
|------|---------|
| 多线程 | `Thread`, `threading`, `pthread` |
| 异步 | `async`, `await`, `Promise`, `Future` |
| 协程 | `coroutine`, `goroutine`, `asyncio` |
| 事件循环 | `EventLoop`, `loop`, `run_loop` |
| 锁 | `Lock`, `Mutex`, `Semaphore` |
| 线程池 | `ThreadPool`, `ExecutorService` |

### 安全特征

| 特征 | 识别方式 |
|------|---------|
| 认证 | `auth`, `login`, `token`, `jwt` |
| 授权 | `permission`, `role`, `acl` |
| 加密 | `encrypt`, `decrypt`, `crypto`, `hash` |
| HTTPS | `https`, `ssl`, `tls` |
| CORS | `cors`, `Cross-Origin` |

## 分析策略

### 优先级

1. **配置文件优先**：先检查配置文件确定语言和框架
2. **目录结构次之**：通过目录结构确认架构模式
3. **代码特征最后**：深入代码分析具体实现

### 多语言项目

对于多语言项目（如前后端分离、Monorepo）：
1. 分别识别各部分的语言
2. 分析各部分的架构
3. 分析跨语言的数据流和通信

### 未知语言处理

遇到未知语言或配置：
1. 查看文件扩展名
2. 查看文件内容特征（语法、关键字）
3. 查看项目文档（README、CONTRIBUTING）
4. 使用 Claude 的通用代码理解能力分析