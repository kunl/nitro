<script setup lang="ts">
const { data: page } = await useAsyncData('index', () => queryCollection('content').path('/').first())
if (!page.value) {
  throw createError({ statusCode: 404, statusMessage: 'Page not found', fatal: true })
}

const title = page.value.seo?.title || page.value.title
const description = page.value.seo?.description || page.value.description

usePageSEO({
  title: title,
  description: description,
  keywords: ['Nitro', 'Vite', '全栈', '部署', '托管平台', 'Nitro 中文文档'],
})
</script>

<template>
  <ContentRenderer
    v-if="page"
    :value="page"
    :prose="false"
  />
</template>
