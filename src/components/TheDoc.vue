<script setup>
// 只保留空的 script 标签
</script>

<template>
  <!-- 只保留最外层容器，不要任何背景色或遮罩 -->
  <div class="doc">
    <slot />
  </div>
</template>

<style lang="scss" scoped>
.doc {
  min-height: 100vh;
  // 移除 background-color 和 ::before 遮罩代码
}
</style>
