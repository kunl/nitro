# Vercel

> 将 Nitro 应用部署到 Vercel。

**Preset：** `vercel`

:read-more{title="Vercel 框架支持" to="https://vercel.com/docs/frameworks"}

::note
可以通过[零配置](/deploy/#zero-config-providers)与此提供商集成。
::

## 入门

部署到 Vercel 具有以下功能：
- [预览部署](https://vercel.com/docs/deployments/environments)
- [Fluid compute](https://vercel.com/docs/fluid-compute)
- [可观测性](https://vercel.com/docs/observability)
- [Vercel 防火墙](https://vercel.com/docs/vercel-firewall)

等等。在 [Vercel 文档](https://vercel.com/docs) 中了解更多。

### 使用 Git 部署

Vercel 以零配置支持 Nitro。[立即将 Nitro 部署到 Vercel](https://vercel.com/new/clone?repository-url=https%3A%2F%2Fgithub.com%2Fvercel%2Fvercel%2Ftree%2Fmain%2Fexamples%2Fnitro)。

## API 路由

Nitro 的 `/api` 目录与 Vercel 不兼容。相反，你应该使用：

- `routes/api/` 用于独立使用

## Bun runtime

:read-more{title="Vercel" to="https://vercel.com/docs/functions/runtimes/bun"}

通过在 `nitro.config` 内使用 `vercel.functions` 键指定 runtime 来使用 [Bun](https://bun.com) 代替 Node.js：

```ts [nitro.config.ts]
export default defineNitroConfig({
  vercel: {
    functions: {
      runtime: "bun1.x"
    }
  }
})
```

或者，如果你在 `vercel.json` 中指定了 `bunVersion` 属性，Nitro 也会自动检测 Bun：

```json [vercel.json]
{
  "$schema": "https://openapi.vercel.sh/vercel.json",
  "bunVersion": "1.x"
}
```

## 自定义构建输出配置

使用 `nitro.config` 内的 `vercel.config` 键提供额外的[构建输出配置](https://vercel.com/docs/build-output-api/v3)。它将与内置的自动生成配置合并。

## 按需增量静态重新生成 (ISR)

按需重新验证允许你随时清除 ISR 路由的缓存，而不需要后台重新验证所需的时间间隔。

要按需重新验证页面：

1. 创建一个环境变量，用于存储重新验证密钥
   - 你可以使用命令 `openssl rand -base64 32` 或[生成密钥](https://generate-secret.vercel.app/32) 来生成随机值。

2. 更新你的配置：

    ```ts [nitro.config.ts]
    import { defineNitroConfig } from "nitro/config";

    export default defineNitroConfig({
      vercel: {
        config: {
          bypassToken: process.env.VERCEL_BYPASS_TOKEN
        }
      }
    })
    ```

3. 要触发"按需增量静态重新生成 (ISR)"并重新验证预渲染函数的路径，向该路径发出带有 x-prerender-revalidate: `bypassToken` 头的 GET 或 HEAD 请求。当使用此头访问该预渲染函数端点时，缓存将被重新验证。对该函数的下一个请求应返回新鲜响应。

### 通过路由规则进行细粒度 ISR 配置

默认情况下，缓存会忽略查询参数。

向 `isr` 路由规则传递选项对象来配置缓存行为。

- `expiration`：缓存资产将被调用无服务器函数重新生成之前的过期时间（以秒为单位）。将值设置为 `false`（或 `isr: true` 路由规则）意味着它永远不会过期。
- `group`：资产的组号。具有相同组号的预渲染资产将同时重新验证。
- `allowQuery`：将独立缓存的查询字符串参数名称列表。
  - 如果是空数组，查询值不考虑用于缓存。
  - 如果是 `undefined`，每个唯一的查询值都独立缓存。
  - 对于通配符 `/**` 路由规则，始终添加 `url`

- `passQuery`：当为 `true` 时，查询字符串将出现在传递给调用函数的 `request` 参数中。`allowQuery` 过滤器仍然适用。

```ts
export default defineNitroConfig({
  routeRules: {
    "/products/**": {
      isr: {
        allowQuery: ["q"],
        passQuery: true,
      },
    },
  },
});
```