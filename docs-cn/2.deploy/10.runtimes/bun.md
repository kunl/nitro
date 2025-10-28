---
icon: simple-icons:bun
---

# Bun

> 使用 Bun runtime 运行 Nitro 应用。

**Preset：** `bun`

Nitro 输出与 Bun runtime 兼容。虽然使用默认的 [Node.js](/deploy/runtimes/node)，你也可以在 bun 中运行输出，使用 `bun` preset 具有更好优化的优势。

使用 `bun` 作为 preset 构建后，你可以使用以下命令在生产环境中运行服务器：

```bash
bun run ./.output/server/index.mjs
```

:read-more{to="https://bun.sh"}