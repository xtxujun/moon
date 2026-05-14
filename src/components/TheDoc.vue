<script setup>
// 保持空
</script>

<template>
  <div class="doc">
    <slot />
  </div>
</template>

<style scoped>
/* 关键：必须是完全透明的容器 */
.doc {
  min-height: 100vh;
  background-color: transparent !important; /* 强制透明 */
}
</style>
