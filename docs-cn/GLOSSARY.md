---
icon: i-lucide-book-open
---

# Nitro 中文文档术语表

本文档列出了 Nitro 文档翻译中需要保持英文原文的术语和需要翻译的术语。

---

## 保持英文原文的术语

### 核心技术术语

| 英文术语 | 说明 | 示例用法 |
|---------|------|---------|
| Runtime | 运行时环境 | Nitro 兼容任何 runtime |
| Server Route | 服务器路由 | 在 `routes/` 目录创建 server route |
| API Route | API 路由 | 添加 API route 处理请求 |
| Handler | 处理函数 | 使用 `defineHandler` 创建 handler |
| Middleware | 中间件 | 添加 middleware 处理请求 |
| Preset | 预设配置 | 使用 `standard` preset |
| Provider | 部署平台/提供商 | 部署到不同的 provider |
| Cache | 缓存 | 使用 cache 提升性能 |
| Storage | 存储层 | Nitro 提供 key-value storage |
| Database | 数据库 | 内置 SQL database 支持 |
| Plugin | 插件 | 通过 plugin 扩展功能 |
| Task | 任务 | 定义后台 task |
| Asset | 静态资源 | 处理 asset 文件 |
| Renderer | 渲染器 | 配置 HTML renderer |
| Lifecycle | 生命周期 | Nitro lifecycle hooks |
| Configuration | 配置 | 修改 configuration 选项 |

### Web 标准术语

| 英文术语 | 说明 | 示例用法 |
|---------|------|---------|
| HMR | Hot Module Replacement | 开发时支持 HMR |
| SSR | Server-Side Rendering | 启用 SSR 模式 |
| ISR | Incremental Static Regeneration | 使用 ISR 策略 |
| SWR | Stale While Revalidate | 配置 SWR cache |
| ESR | Edge Side Rendering | 在 edge 上使用 ESR |
| CORS | Cross-Origin Resource Sharing | 配置 CORS 策略 |
| API Token | API 令牌 | 使用 API token 认证 |

### 框架和库

| 名称 | 类型 | 说明 |
|------|------|------|
| Nitro | 框架 | 本项目名称 |
| Vite | 构建工具 | 前端构建工具 |
| Vue | 前端框架 | Vue.js 框架 |
| React | 前端框架 | React 框架 |
| Svelte | 前端框架 | Svelte 框架 |
| Nuxt | 元框架 | 基于 Vue 的元框架 |
| SolidStart | 元框架 | 基于 Solid 的元框架 |
| TanStack Start | 元框架 | TanStack 的元框架 |
| h3 | HTTP 框架 | 轻量级 HTTP 框架 |
| Hono | HTTP 框架 | 快速 Web 框架 |
| Elysia | HTTP 框架 | TypeScript Web 框架 |

### Runtime 环境

| 名称 | 说明 |
|------|------|
| Node.js | JavaScript runtime |
| Bun | 高性能 JavaScript runtime |
| Deno | 安全的 JavaScript/TypeScript runtime |

### 云平台和服务

| 名称 | 类型 |
|------|------|
| Cloudflare Workers | Serverless 平台 |
| Vercel | 部署平台 |
| Netlify | 部署平台 |
| AWS | 云服务 |
| Azure | 云服务 |
| Firebase | 云服务 |
| GitHub Pages | 静态托管 |
| GitLab Pages | 静态托管 |
| Heroku | 应用平台 |
| DigitalOcean | 云服务 |
| Render | 部署平台 |
| Zeabur | 部署平台 |
| Deno Deploy | 部署平台 |

### 数据库和存储

| 名称 | 类型 |
|------|------|
| SQLite | 数据库 |
| PostgreSQL / Postgres | 数据库 |
| MySQL | 数据库 |
| PGLite | 数据库 |
| Redis | 缓存/数据库 |
| S3 | 对象存储 |

### 编程语言和工具

| 名称 | 说明 |
|------|------|
| TypeScript | 编程语言 |
| JavaScript | 编程语言 |
| npm / pnpm / yarn | 包管理器 |
| Git | 版本控制 |

### 文件和目录名称

所有文件名、目录名、路径保持英文原文：

- `routes/`
- `server.ts`
- `vite.config.ts`
- `.output/`
- `package.json`
- `node_modules/`
- `public/`

### 代码相关

所有代码、命令、配置项保持英文原文：

- `defineHandler`
- `fetch`
- `export default`
- `import`
- 函数名、变量名、类名等

---

## 需要翻译的术语

### 常见翻译对照

| 英文 | 中文 | 说明 |
|------|------|------|
| Introduction | 介绍 | - |
| Quick Start | 快速开始 | - |
| Guide | 指南 | - |
| Tutorial | 教程 | - |
| Documentation | 文档 | - |
| Overview | 概览 | - |
| Getting Started | 开始使用 | - |
| Installation | 安装 | - |
| Deployment | 部署 | - |
| Development | 开发 | - |
| Production | 生产环境 | - |
| Build | 构建 | - |
| Deploy | 部署（动词） | - |
| Configure | 配置（动词） | - |
| Migration | 迁移 | - |
| Routing | 路由 | 作为章节标题时翻译 |
| Feature | 特性/功能 | 根据上下文选择 |
| Full-stack | 全栈 | - |
| Frontend | 前端 | - |
| Backend | 后端 | - |
| Server | 服务器 | 作为描述性词汇时翻译 |
| Client | 客户端 | 作为描述性词汇时翻译 |
| Application | 应用/应用程序 | - |
| Project | 项目 | - |
| Directory | 目录 | - |
| File | 文件 | - |
| Folder | 文件夹 | - |
| Code | 代码 | - |
| Example | 示例 | - |
| Usage | 用法 | - |
| Options | 选项 | - |
| Parameters | 参数 | - |

---

## 翻译原则

### 1. 优先保持英文的情况

- **技术术语**：Runtime、Cache、Storage 等核心技术概念
- **专有名词**：框架名、平台名、工具名等
- **代码内容**：所有代码、命令、配置项
- **文件路径**：所有文件名、目录名

### 2. 需要翻译的情况

- **描述性文字**：解释说明、使用指南
- **章节标题**：如"快速开始"、"部署指南"
- **概念解释**：对技术概念的说明文字
- **操作步骤**：具体的使用步骤说明

### 3. 中英文混排规范

```markdown
✅ 正确：Nitro 是一个全栈框架，兼容任何 runtime。
❌ 错误：Nitro是一个全栈框架，兼容任何runtime。

✅ 正确：在 `routes/` 目录中创建 server route
❌ 错误：在`routes/`目录中创建server route

✅ 正确：使用 `defineHandler` 函数定义 handler
❌ 错误：使用`defineHandler`函数定义handler
```

规则：
- 中文与英文术语之间添加空格
- 中文与代码（反引号包裹）之间添加空格
- 英文术语与标点符号之间不需要空格

### 4. 标点符号使用

- 中文段落使用中文标点：，。；：？！
- 英文术语、代码周围使用英文标点
- 列表项结尾通常不加标点

---

## 术语使用示例

### 示例 1：保持术语原文

**原文**：
```markdown
Nitro is a full-stack framework, compatible with any runtime. It extends your Vite application with a production-ready server.
```

**译文**：
```markdown
Nitro 是一个全栈框架，兼容任何 runtime。它为你的 Vite 应用扩展了一个生产就绪的 server。
```

### 示例 2：混合使用

**原文**：
```markdown
Create server routes in the routes/ folder and they will be automatically registered.
```

**译文**：
```markdown
在 `routes/` 目录中创建 server route，它们将会被自动注册。
```

### 示例 3：章节标题

**原文**：
```markdown
## Quick Start
```

**译文**：
```markdown
## 快速开始
```

**原文**：
```markdown
## Server Routes
```

**译文**：
```markdown
## Server Routes
```
（章节标题如果包含技术术语，可保持原文或部分翻译）

---

## 贡献指南

如果你在翻译过程中遇到本术语表未涵盖的术语：

1. **优先查阅**：
   - [Vite 中文文档](https://cn.vitejs.dev)的术语使用
   - [Vue 中文文档](https://cn.vuejs.org)的术语使用
   - 其他知名项目的中文文档

2. **添加到术语表**：
   - 在相应章节添加新术语
   - 说明翻译原因或参考依据
   - 提交 PR 更新术语表

3. **讨论不确定的术语**：
   - 在 Issue 中提出讨论
   - 征求其他译者意见
   - 达成共识后更新术语表

---

最后更新：2025-10-28
