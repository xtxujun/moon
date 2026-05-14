<script setup>
// 保持空
</script>

<template>
  <div class="doc">
    <slot />
  </div>
</template>

<!-- 关键：删除所有全局样式！只保留容器透明 -->
<style scoped>
.doc {
  min-height: 100vh;
  background-color: transparent !important; /* 仅容器透明 */
}
</style>
