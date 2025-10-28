# Netlify

> 将 Nitro 应用部署到 Netlify functions 或 edge。

**Preset：** `netlify`

:read-more{title="Netlify Functions" to="https://www.netlify.com/platform/core/functions/"}

::note
可以通过[零配置](/deploy/#zero-config-providers)与此提供商集成。
::

通常，部署到 Netlify 不需要任何配置。
Nitro 将自动检测你处于 [Netlify](https://www.netlify.com) 构建环境中，并构建服务器的正确版本。

对于新站点，Netlify 将检测你正在使用 Nitro 并将发布目录设置为 `dist`，构建命令设置为 `npm run build`。

如果你正在升级现有站点，你应该检查这些并在需要时更新它们。

如需添加自定义重定向，使用 [`routeRules`](/config#routerules) 或通过将 [`_redirects`](https://docs.netlify.com/routing/redirects/#syntax-for-the-redirects-file) 文件添加到 `public` 目录来实现。

对于部署，只需推送到你的 git 仓库，[就像你通常为 Netlify 所做的那样](https://docs.netlify.com/configure-builds/get-started/)。

::note{type="note"}
创建新项目时，确保发布目录设置为 `dist`。
::

## Netlify edge functions

**Preset：** `netlify_edge`

Netlify Edge Functions 使用 Deno 和强大的 V8 JavaScript runtime，让你运行全局分布的函数，以获得最快的响应时间。

:read-more{title="Netlify Edge functions" to="https://docs.netlify.com/edge-functions/overview/"}

Nitro 输出可以直接在边缘运行服务器。更接近你的用户。

::note{type="note"}
创建新项目时，确保发布目录设置为 `dist`。
::

## 自定义部署配置

使用 `nitro.config` 内的 `netlify` 键提供额外的部署配置。它将与内置的自动生成配置合并。目前唯一支持的值是 `images.remote_images`，用于[配置 Netlify Image CDN](https://docs.netlify.com/image-cdn/create-integration/)。