<script setup lang="ts">
// 1. 引入组件
import BingBackground from './components/BingBackground.vue'
// ... 其他原有的引入
</script>

<template>
  <!-- 2. 放置背景组件 (放在最前面) -->
  <BingBackground />

  <!-- 原有的页面内容 -->
  <div class="app-container">
     <!-- ... 原有代码 ... -->
  </div>
</template>
