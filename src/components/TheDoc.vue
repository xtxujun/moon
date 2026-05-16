<script setup>
// 这里暂时不需要逻辑
</script>

<template>
  <div class="min-h-screen flex flex-col">
    <!-- 插槽：承载 index.vue 的内容 -->
    <slot />
  </div>
</template>

<style scoped>
/* 确保没有任何背景色干扰 */
</style>
