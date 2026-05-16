<script setup>
// 逻辑留空
</script>

<template>
  <div class="doc">
    <slot />
  </div>
</template>

<style scoped>
.doc {
  min-height: 100vh;
  /* 确保这里没有任何背景色，完全透明 */
  background-color: transparent;
}
</style>
