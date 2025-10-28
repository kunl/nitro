# Cloudflare

> 将 Nitro 应用部署到 Cloudflare。

## Cloudflare Workers

**Preset：** `cloudflare_module`

:read-more{title="Cloudflare Workers" to="https://developers.cloudflare.com/workers/"}

::note
可以通过[零配置](/deploy#zero-config-providers)与此提供商集成，支持[workers builds (beta)](https://developers.cloudflare.com/workers/ci-cd/builds/)。
::

::important
要使用带有静态资源的 Workers，你需要将 Nitro 兼容性日期设置为 `2024-09-19` 或更晚。
::

以下显示了将 Nitro 应用部署到 Cloudflare Workers 的示例 `nitro.config.ts` 文件。

```ts [nitro.config.ts]
import { defineNitroConfig } from "nitro/config";

export default defineNitroConfig({
    compatibilityDate: "2024-09-19",
    preset: "cloudflare_module",
    cloudflare: {
      deployConfig: true,
      nodeCompat: true
    }
})
```

通过设置 `deployConfig: true`，Nitro 将自动为你生成具有正确配置的 `wrangler.json`。
如果你需要添加 [Cloudflare Workers 配置](https://developers.cloudflare.com/workers/wrangler/configuration/)，例如[绑定](https://developers.cloudflare.com/workers/runtime-apis/bindings/)，你可以：

- 在你的 Nitro 配置中设置这些，位于 `cloudflare: { wrangler : {} }` 下。这与 `wrangler.json` 具有相同的类型。
- 提供你自己的 `wrangler.json`。Nitro 将你的配置与适当的设置合并，包括指向构建输出。

### 本地预览

你可以使用 [Wrangler](https://github.com/cloudflare/workers-sdk/tree/main/packages/wrangler) 在本地预览你的应用：

:pm-run{script="build"}

:pm-x{command="wrangler dev"}

### 手动部署

构建应用程序后，你可以使用 Wrangler 手动部署。

首先确保已登录到你的 Cloudflare 账户：

:pm-x{command="wrangler login"}

然后你可以使用以下命令部署应用程序：

:pm-x{command="wrangler deploy"}

### Runtime Hooks

你可以在下面使用 [runtime hooks](/docs/plugins#nitro-runtime-hooks) 来扩展 [Worker handlers](https://developers.cloudflare.com/workers/runtime-apis/handlers/)。

:read-more{to="/guide/plugins#nitro-runtime-hooks"}

- [`cloudflare:scheduled`](https://developers.cloudflare.com/workers/runtime-apis/handlers/scheduled/)
- [`cloudflare:email`](https://developers.cloudflare.com/email-routing/email-workers/runtime-api/)
- [`cloudflare:queue`](https://developers.cloudflare.com/queues/configuration/javascript-apis/#consumer)
- [`cloudflare:tail`](https://developers.cloudflare.com/workers/runtime-apis/handlers/tail/)
- `cloudflare:trace`


## Cloudflare Pages

**Preset：** `cloudflare_pages`

:read-more{title="Cloudflare Pages" to="https://pages.cloudflare.com/"}

::note
可以通过[零配置](/deploy#zero-config-providers)与此提供商集成。
::

::warning
Cloudflare [Workers Module](#cloudflare-workers) 是新的推荐部署 preset。请仅在需要特定功能时考虑使用 pages。
::

以下显示了将 Nitro 应用部署到 Cloudflare Pages 的示例 `nitro.config.ts` 文件。

```ts [nitro.config.ts]
import { defineNitroConfig } from "nitro/config";

export default defineNitroConfig({
    preset: "cloudflare_pages",
    cloudflare: {
      deployConfig: true,
      nodeCompat:true
    }
})
```

Nitro 自动生成一个 `_routes.json` 文件，控制哪些路由从文件提供服务，哪些从 Worker 脚本提供服务。可以使用配置选项 `cloudflare.pages.routes` 覆盖自动生成的路由文件（[阅读更多](https://developers.cloudflare.com/pages/platform/functions/routing/#functions-invocation-routes)）。

### 本地预览

你可以使用 [Wrangler](https://github.com/cloudflare/workers-sdk/tree/main/packages/wrangler) 在本地预览你的应用：

:pm-run{script="build"}

:pm-x{command="wrangler pages dev"}

### 手动部署

构建应用程序后，你可以使用 Wrangler 手动部署，为此首先确保已登录到你的 Cloudflare 账户：

:pm-x{command="wrangler login"}

然后你可以使用以下命令部署应用程序：

:pm-x{command="wrangler pages deploy"}


## 使用 GitHub Actions 在 CI/CD 中部署

无论你使用 Cloudflare Pages 还是 Cloudflare Workers，你都可以使用 [Wrangler GitHub actions](https://github.com/marketplace/actions/deploy-to-cloudflare-workers-with-wrangler) 部署你的应用程序。

::note
**注意：** 记住[指示 Nitro 使用正确的 preset](/deploy#changing-the-deployment-preset)（请注意，这对于所有 preset 都是必需的，包括 `cloudflare_pages`）。
::

## 环境变量

Nitro 允许你使用 `process.env` 或 `import.meta.env` 或 runtime config 全局访问环境变量。

::note
确保只在**事件生命周期内**访问环境变量，而不是在全局上下文中，因为 Cloudflare 只在请求生命周期期间而不是之前使它们可用。
::

**示例：** 如果你设置了 `SECRET` 和 `NITRO_HELLO_THERE` 环境变量，你可以通过以下方式访问它们：

```ts
import { defineHandler } from "nitro/h3";

console.log(process.env.SECRET) // 注意这是在全局作用域中！所以它实际上不起作用，变量是 undefined！

export default defineHandler((event) => {
  // 注意以下所有都是访问上述变量的有效方式
  useRuntimeConfig(event).helloThere
  useRuntimeConfig(event).secret
  process.env.NITRO_HELLO_THERE
  import.meta.env.SECRET
});
```

### 在开发模式中指定变量

对于开发，你可以使用 `.env` 或 `.env.local` 文件来指定环境变量：

```ini
NITRO_HELLO_THERE="captain"
SECRET="top-secret"
```

::note
**注意：** 确保将 `.env` 和 `.env.local` 添加到 `.gitignore` 文件中，这样你就不会提交它，因为它可能包含敏感信息。
::

### 为本地预览指定变量

构建后，当你使用 `wrangler dev` 或 `wrangler pages dev` 在本地尝试你的项目时，为了能够访问环境变量，你需要在项目根目录中的 `.dev.vars` 文件中指定它们（如 [Pages](https://developers.cloudflare.com/pages/functions/bindings/#interact-with-your-environment-variables-locally) 和 [Workers](https://developers.cloudflare.com/workers/configuration/environment-variables/#interact-with-environment-variables-locally) 文档中所述）。

如果你在开发时使用 `.env` 或 `.env.local` 文件，你的 `.dev.vars` 应该与它相同。

::note
**注意：** 确保将 `.dev.vars` 添加到 `.gitignore` 文件中，这样你就不会提交它，因为它可能包含敏感信息。
::

### 为生产指定变量

对于生产，使用 Cloudflare 仪表板或 [`wrangler secret`](https://developers.cloudflare.com/workers/wrangler/commands/#secret) 命令来设置环境变量和密钥。

### 使用 `wrangler.toml`/`wrangler.json` 指定变量

你可以指定自定义 `wrangler.toml`/`wrangler.json` 文件并在内部定义变量。

::warning
注意，对于像密钥这样的敏感数据，不建议这样做。
::

**示例：**

```ini [wrangler.toml]
# 共享
[vars]
NITRO_HELLO_THERE="general"
SECRET="secret"

# 覆盖 `--env production` 使用的值
[env.production.vars]
NITRO_HELLO_THERE="captain"
SECRET="top-secret"
```

## 直接访问 Cloudflare 绑定

绑定允许你与 Cloudflare 平台的资源交互，此类资源的示例是键值数据存储（[KVs](https://developers.cloudflare.com/kv/)）和无服务器 SQL 数据库（[D1s](https://developers.cloudflare.com/d1/)）。

::read-more
有关绑定及其使用的更多详细信息，请参阅 Cloudflare [Pages](https://developers.cloudflare.com/pages/functions/bindings/) 和 [Workers](https://developers.cloudflare.com/workers/configuration/bindings/#bindings) 文档。
::

> [!TIP]
> Nitro 提供了高级 API 来与诸如 [KV Storage](/docs/storage) 和 [Database](/docs/database) 等原语交互，强烈建议优先使用它们，而不是直接依赖低级 API 以确保使用稳定性。

:read-more{title="数据库层" to="/docs/database"}

:read-more{title="KV 存储" to="/docs/storage"}

在 runtime 中，你可以通过访问请求事件的 `context.cloudflare.env` 字段来访问绑定，例如，这是你访问 D1 绑定的方式：

```ts
import { defineHandler } from "nitro/h3";

defineHandler(async (event) => {
  const { cloudflare } = event.context
  const stmt = await cloudflare.env.MY_D1.prepare('SELECT id FROM table')
  const { results } = await stmt.all()
})
```

### 在本地开发中访问绑定

> [!NOTE]
> `nitro-cloudflare-dev` 模块是实验性的。Nitro 团队正在研究更原生的集成，这可能在不久的将来使该模块变得不必要。

为了在开发模式中访问绑定，我们首先定义绑定。你可以在 `wrangler.toml`/`wrangler.json` 文件中执行此操作，或者直接在你的 Nitro 配置中位于 `cloudflare.wrangler` 下（接受与 `wrangler.json` 相同的类型）。

例如，在 `wrangler.toml` 中定义变量和 KV 命名空间

```ini [wrangler.toml]
[vars]
MY_VARIABLE="my-value"

[[kv_namespaces]]
binding = "MY_KV"
id = "xxx"
```

或者在你的 Nitro 配置中：


```js [nitro.config.js]
import { defineNitroConfig } from "nitro/config";
import nitroCloudflareBindings from "nitro-cloudflare-dev";

export default defineNitroConfig({
    cloudflare: {
      wrangler: {
        vars: {
          MY_VARIABLE: "my-value"
        },
        kv_namespaces: [
          {
            binding: "MY_KV",
            id: "xxx"
          }
        ]
      }
    }
});
```

> [!NOTE]
> 只有默认环境中的绑定被识别。

接下来我们安装 `nitro-cloudflare-dev` 模块以及所需的 `wrangler` 包（如果尚未安装）：

:pm-install{name="-D nitro-cloudflare-dev wrangler"}

然后定义模块：

```js [nitro.config.js]
import nitroCloudflareBindings from "nitro-cloudflare-dev";

export default defineNitroConfig({
  modules: [nitroCloudflareBindings],
});
```

从这一刻起，当运行

:pm-run{script="dev"}

你将能够从请求事件访问 `MY_VARIABLE` 和 `MY_KV`，如上所示。