# Deno Deploy

> 将 Nitro 应用部署到 [Deno Deploy](https://deno.com/deploy)。

**Preset：** `deno_deploy`

:read-more{title="Deno Deploy" to="https://deno.com/deploy"}

## 使用 CLI 部署

你可以使用 [deployctl](https://deno.com/deploy/docs/deployctl) 部署你的应用。

登录 [Deno Deploy](https://dash.deno.com/account#access-tokens) 获取 `DENO_DEPLOY_TOKEN` 访问令牌，并将其设置为环境变量。

```bash
# 使用 deno_deploy NITRO preset 构建
NITRO_PRESET=deno_deploy npm run build

# 确保从输出目录运行 deployctl 命令
cd .output
deployctl deploy --project=my-project server/index.ts
```

## 使用 GitHub actions 在 CI/CD 中部署

你只需要在工作流中包含 deployctl GitHub Action 作为步骤。

你不需要为此设置任何密钥。你需要将你的 GitHub 仓库链接到你的 Deno Deploy 项目并选择"GitHub Actions"部署模式。你可以在 [Deno Deploy](https://dash.deno.com) 上的项目设置中执行此操作。

在你的 `.github/workflows` 目录中创建以下工作流文件：

```yaml [.github/workflows/deno_deploy.yml]
name: deno-deploy

on:
  push:
    branches:
      - main
  pull_request:
    branches:
      - main

jobs:
  deploy:
    steps:
      - uses: actions/checkout@v5
      - run: corepack enable
      - uses: actions/setup-node@v5
        with:
          node-version: 18
          cache: pnpm
      - run: pnpm install
      - run: pnpm build
        env:
          NITRO_PRESET: deno_deploy
      - name: Deploy to Deno Deploy
        uses: denoland/deployctl@v1
        with:
          project: my-project
          entrypoint: server/index.ts
          root: .output
```

## Deno runtime

:read-more{to="/deploy/runtimes/deno"}