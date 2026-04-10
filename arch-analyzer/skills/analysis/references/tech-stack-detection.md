# 技术栈检测规则

## 检测流程

### Step 1: 文件扩展名扫描

扫描项目目录，统计文件扩展名分布：
- 主要语言：文件数最多的语言
- 辅助语言：其他语言（如配置文件、脚本）

### Step 2: 配置文件分析

检查配置文件，确定框架和依赖：
- 依赖文件：package.json、requirements.txt 等
- 构建配置：tsconfig.json、pyproject.toml 等
- 框架特征：特定框架的配置文件

### Step 3: 代码特征分析

分析源代码，确认框架和库：
- import/require 语句
- 特定框架的代码模式
- 注释和文档中的框架名称

## 语言检测规则

### 主要语言识别

| 语言 | 主要特征 |
|------|---------|
| Python | .py 文件，requirements.txt/pyproject.toml |
| JavaScript | .js 文件，package.json |
| TypeScript | .ts/.tsx 文件，tsconfig.json |
| Java | .java 文件，pom.xml/build.gradle |
| Go | .go 文件，go.mod |
| Rust | .rs 文件，Cargo.toml |
| Ruby | .rb 文件，Gemfile |
| PHP | .php 文件，composer.json |
| C/C++ | .c/.cpp/.h 文件，CMakeLists.txt/Makefile |
| C# | .cs 文件，*.csproj |
| Swift | .swift 文件，Package.swift |
| Kotlin | .kt 文件，build.gradle.kts |

### 多语言项目处理

对于多语言项目：
1. 分别统计各语言文件数
2. 确定主语言（文件数最多）
3. 确定辅助语言（配置、脚本、测试等）
4. 分析跨语言交互方式

## 框架检测规则

### Web 框架

| 框架 | 检测特征 |
|------|---------|
| Django | `django` in requirements.txt, `manage.py`, `settings.py` |
| FastAPI | `fastapi` in requirements.txt, `from fastapi import` |
| Flask | `flask` in requirements.txt, `from flask import` |
| Express | `express` in package.json, `require('express')` |
| NestJS | `@nestjs/core` in package.json, `@Module` decorator |
| Next.js | `next` in package.json, `pages/` or `app/` directory |
| Nuxt.js | `nuxt` in package.json, `pages/` directory |
| Spring Boot | `spring-boot` in pom.xml, `@SpringBootApplication` |
| Rails | `rails` in Gemfile, `app/controllers/` |
| Laravel | `laravel/framework` in composer.json |
| Gin | `github.com/gin-gonic/gin` in go.mod |
| Actix | `actix-web` in Cargo.toml |

### 前端框架

| 框架 | 检测特征 |
|------|---------|
| React | `react` in package.json, `.jsx/.tsx` files |
| Vue | `vue` in package.json, `.vue` files |
| Angular | `@angular/core` in package.json, `*.module.ts` |
| Svelte | `svelte` in package.json, `.svelte` files |
| Solid | `solid-js` in package.json |

### 移动框架

| 框架 | 检测特征 |
|------|---------|
| React Native | `react-native` in package.json |
| Flutter | `flutter` in pubspec.yaml, `.dart` files |
| Ionic | `@ionic/core` in package.json |

### ORM/数据库

| 工具 | 检测特征 |
|------|---------|
| SQLAlchemy | `sqlalchemy` in requirements.txt |
| Prisma | `prisma` in package.json, `prisma/schema.prisma` |
| TypeORM | `typeorm` in package.json |
| Sequelize | `sequelize` in package.json |
| JPA | `javax.persistence` imports |
| GORM | `gorm` in go.mod |
| Entity Framework | `EntityFrameworkCore` in *.csproj |

## 构建工具检测

| 工具 | 检测特征 |
|------|---------|
| npm | package.json, package-lock.json |
| yarn | package.json, yarn.lock |
| pnpm | package.json, pnpm-lock.yaml |
| pip | requirements.txt |
| poetry | pyproject.toml (with poetry config) |
| pipenv | Pipfile |
| Maven | pom.xml |
| Gradle | build.gradle, build.gradle.kts |
| Make | Makefile |
| CMake | CMakeLists.txt |
| Cargo | Cargo.toml |
| Go build | go.mod |
| Bundler | Gemfile |
| Composer | composer.json |
| sbt | build.sbt |
| Mix | mix.exs |
| NuGet | *.csproj, packages.config |

## 测试框架检测

| 框架 | 检测特征 |
|------|---------|
| pytest | `pytest` in requirements.txt, `test_*.py` |
| unittest | `unittest` imports, `test_*.py` |
| Jest | `jest` in package.json, `*.test.js` |
| Mocha | `mocha` in package.json, `test/` |
| Vitest | `vitest` in package.json, `*.test.ts` |
| JUnit | `junit` in pom.xml, `Test*.java` |
| Go test | `_test.go` files |
| Rust test | `#[test]` attributes |
| RSpec | `rspec` in Gemfile, `*_spec.rb` |

## 依赖分析

### 依赖文件解析

1. 读取依赖文件
2. 解析依赖列表
3. 分类依赖：
   - 生产依赖（dependencies）
   - 开发依赖（devDependencies）
   - 可选依赖（optionalDependencies）

### 依赖分类

| 类型 | 说明 |
|------|------|
| 核心框架 | 主要框架（如 React、Django） |
| 工具库 | 辅助工具（如 lodash、requests） |
| 开发工具 | 开发依赖（如 eslint、pytest） |
| 测试工具 | 测试框架（如 jest、pytest） |
| 构建工具 | 构建相关（如 webpack、vite） |

## 代码规模统计

### 统计指标

| 指标 | 说明 |
|------|------|
| 总文件数 | 项目中所有文件数量 |
| 源代码文件数 | 源代码文件数量 |
| 总代码行数 | 所有源代码行数 |
| 按语言统计 | 各语言的文件数和行数 |
| 注释比例 | 注释行数占比 |

### 统计方法

1. 扫描项目目录
2. 按扩展名分类文件
3. 统计各类型文件数
4. 统计代码行数（排除空行和注释）

## 输出格式

### tech-stack.json 结构

```json
{
  "languages": [
    {
      "name": "Python",
      "file_count": 50,
      "line_count": 5000,
      "percentage": 80
    },
    {
      "name": "JavaScript",
      "file_count": 10,
      "line_count": 1000,
      "percentage": 20
    }
  ],
  "primary_language": "Python",
  "frameworks": [
    {
      "name": "FastAPI",
      "type": "web",
      "version": "0.100.0"
    }
  ],
  "build_tools": [
    {
      "name": "pip",
      "config_file": "requirements.txt"
    }
  ],
  "test_frameworks": [
    {
      "name": "pytest",
      "config_file": "pyproject.toml"
    }
  ],
  "dependencies": {
    "production": [
      {
        "name": "fastapi",
        "version": "0.100.0"
      }
    ],
    "development": [
      {
        "name": "pytest",
        "version": "7.0.0"
      }
    ]
  },
  "code_metrics": {
    "total_files": 60,
    "source_files": 50,
    "total_lines": 6000,
    "source_lines": 5000,
    "comment_lines": 500,
    "blank_lines": 500
  }
}
```

## 检测优先级

1. **配置文件优先**：先检查配置文件，快速确定语言和框架
2. **文件扩展名次之**：统计文件类型分布
3. **代码特征最后**：深入代码确认框架和库的使用

## 特殊情况处理

### Monorepo 项目

- 分别检测各子项目的技术栈
- 汇总整体技术栈信息
- 标注各子项目的技术栈差异

### 混合语言项目

- 检测各语言的技术栈
- 分析跨语言交互方式
- 标注主要语言和辅助语言

### 无配置文件项目

- 通过文件扩展名识别语言
- 通过代码特征识别框架
- 通过目录结构识别架构