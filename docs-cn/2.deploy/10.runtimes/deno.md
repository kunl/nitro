---
icon: simple-icons:deno
---

# Deno

> 使用 [Deno](https://deno.com/) runtime 运行 Nitro 应用。

**Preset：** `deno_server`

你可以使用 Node.js 构建 Nitro 服务器，以便在自定义服务器中的 [Deno Runtime](https://deno.com/runtime) 内运行。

```bash
# 使用 deno NITRO preset 构建
NITRO_PRESET=deno_server npm run build

# 启动生产服务器
deno run --unstable --allow-net --allow-read --allow-env .output/server/index.ts
```

## Deno Deploy

:read-more{to="/deploy/providers/deno-deploy"}