---
seo:
  title: 部署全栈 Vite 应用
  description: Nitro 为你的 Vite 应用扩展了生产级服务器，兼容任何 runtime。为你的应用添加 server routes，零配置部署体验，支持多个托管平台。
---

::u-page-hero
---
orientation: horizontal
---
::code-group
  :::prose-pre
  ---
  filename: vite.config.ts
  ---
  ```ts
  import { defineConfig } from 'vite'
  import { nitro } from 'nitro/vite'

  export default defineConfig({
    plugins: [
      nitro()
    ],
    nitro: {
      preset: 'standard'
    }
  })
  ```
  :::
::

:hero-background

#title
部署[全栈]{.text-primary} Vite 应用

#description
Nitro 为你的 Vite 应用扩展了生产级服务器，兼容任何 runtime。为你的应用添加 server routes，零配置部署体验，支持多个托管平台。

#links
  :::u-button
  ---
  size: xl
  to: /docs/quick-start
  trailing-icon: i-lucide-arrow-right
  ---
  开始使用
  :::

  :::u-button
  ---
  color: neutral
  icon: i-simple-icons-github
  size: xl
  target: _blank
  to: https://github.com/nitrojs/nitro
  variant: outline
  ---
  GitHub
  :::
::

::div{class="bg-neutral-50 dark:bg-neutral-950/30 py-10 border-y border-default"}
  ::u-container
    ::u-page-grid
      ::u-page-feature
      #title
      快速

      #description
      享受 Vite 开发体验，服务器端支持 HMR，并为生产环境优化。
      ::

      ::u-page-feature
      #title
      多功能

      #description
      使用相同代码库，零配置部署到任何平台，不被供应商绑定。
      ::

      ::u-page-feature
      #title
      精简

      #description
      精简设计，以最小开销适配任何解决方案。
      ::

    ::
  ::
::

::u-page-section
---
orientation: horizontal
features:
  - title: 'routes/'
    description: '在 routes/ 文件夹中创建 server routes，它们将被自动注册。'
    icon: 'i-lucide-folder-tree'
  - title: 'server.ts'
    description: '使用完整的 Web 标准，选择你喜欢的标准库，使用 server.ts 文件创建 server routes。'
    icon: 'i-lucide-file-code'
---
#title
创建 Server Routes

#description
开始在 routes/ 文件夹中创建 API routes，或者在 `server.ts` 文件中使用你喜欢的后端框架。

#default
::div{class="min-h-[506px]"}
  ::tabs
    ::tabs-item{label="FS Routing" icon="i-lucide-folder"}
      ::code-tree{defaultValue="routes/hello.ts" expand-all}
        ::prose-pre{filename="vite.config.ts"}
        ```ts
        import { defineConfig } from 'vite'
        import { nitro } from 'nitro/vite'

        export default defineConfig({
          plugins: [
            nitro()
          ],
        });
        ```
        ::
        ::prose-pre{filename="routes/hello.ts"}
        ```ts
        import { defineHandler } from 'nitro/h3'

        export default defineHandler(({ req }) => {
          return { api: 'works!' }
        })
        ```
        ::
        ::prose-pre{filename="index.html"}
        ```html
          <html>
          <head>
            <title>Nitro + Vite</title>
          </head>
          <body>
            <h1>Hey, there!</h1>
          </body>
          </html>
        ```
        ::
      ::
    ::
    ::tabs-item{label="Web Standard" icon="i-lucide-globe"}
      ::prose-pre{filename="server.ts"}
      ```ts
      export default {
        async fetch(req: Request): Promise<Response> {
          return new Response(`Hello world! (${req.url})`);
        },
      };
      ```
      ::
    ::
    ::tabs-item{label="H3" icon="i-undocs-h3"}
      ::prose-pre{filename="server.ts"}
      ```ts
      import { H3 } from 'h3'

      const app = new H3()

      app.get("/", () => '⚡️ Hello from H3!')

      export default app
      ```
      ::
    ::
    ::tabs-item{label="Hono" icon="i-undocs-hono"}
      ::prose-pre{filename="server.ts"}
      ```ts
      import { Hono } from 'hono'

      const app = new Hono()

      app.get("/", (c) => c.text('🔥 Hello from Hono!'))

      export default app
      ```
      ::
    ::
    ::tabs-item{label="Elysia" icon="i-undocs-elysia"}
      ::prose-pre{filename="server.ts"}
      ```ts
      import { Elysia } from 'elysia'

      const app = new Elysia()

      app.get("/", (c) => '🦊 Hello from Elysia!')

      export default app
      ```
      ::
    ::
  ::
::
::

:page-sponsors

:page-contributors