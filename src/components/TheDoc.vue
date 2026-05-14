<script setup>
// 逻辑留空
</script>

<template>
  <div class="doc">
    <slot />
  </div>
</template>

<style scoped>
/* 
   核心修复：
   1. 确保 .doc 容器没有任何背景色
   2. 确保高度撑满，但不遮挡底层背景
*/
.doc {
  min-height: 100vh;
  background-color: transparent !important; /* 强制透明 */
  position: relative; /* 确保层级正常 */
}
</style>
