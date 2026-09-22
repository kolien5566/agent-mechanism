<script setup>
import { computed } from 'vue'
import { useNav } from '@slidev/client'

const { currentPage, total, currentSlideRoute } = useNav()
const isDarkPage = computed(() => /hero-slide|section-dark/.test(String(currentSlideRoute.value?.meta?.class || '')))
const chapter = computed(() => {
  const page = currentPage.value
  if (page <= 4) return 'AI Agent · 原理与使用'
  if (page <= 17) return '01 · 基本机制'
  if (page <= 28) return '02 · 产品与用法'
  if (page <= 51) return '03 · 能力扩展'
  return '04 · 工程演进'
})
</script>

<template>
  <footer v-if="!isDarkPage" class="deck-footer">
    <span>{{ chapter }}</span>
    <span class="page-number">{{ currentPage }} / {{ total }}</span>
  </footer>
</template>
