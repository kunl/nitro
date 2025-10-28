# AWS Lambda

> 将 Nitro 应用部署到 AWS Lambda。

**Preset：** `aws_lambda`

:read-more{title="AWS Lambda" to="https://aws.amazon.com/lambda/"}

Nitro 提供了一个内置 preset，用于生成与 [AWS Lambda](https://aws.amazon.com/lambda/) 兼容的输出格式。
`.output/server/index.mjs` 中的输出入口点与 [AWS Lambda 格式](https://docs.aws.amazon.com/lex/latest/dg/lambda-input-response-format.html) 兼容。

它可以以编程方式使用或作为部署的一部分。

```ts
import { handler } from './.output/server'

// 以编程方式使用
const { statusCode, headers, body } = handler({ rawPath: '/' })
```

## 内联 chunks

Nitro 输出默认使用动态 chunks，仅在需要时延迟加载代码。然而，这有时可能对性能不理想。（参见 [nitrojs/nitro#650](https://github.com/nitrojs/nitro/pull/650) 中的讨论）。你可以使用 [`inlineDynamicImports`](/config#inlinedynamicimports) 配置启用 chunk 内联行为。

```ts [nitro.config.ts]
import { defineNitroConfig } from "nitro/config";

export default defineNitroConfig({
  inlineDynamicImports: true
});
```


## 响应流

:read-more{title="介绍 AWS Lambda 响应流" to="https://aws.amazon.com/blogs/compute/introducing-aws-lambda-response-streaming/"`

为了启用响应流，启用 `awsLambda.streaming` 标志：

```ts [nitro.config.ts]
import { defineNitroConfig } from "nitro/config";

export default defineNitroConfig({
  awsLambda: {
    streaming: true
  }
});
```