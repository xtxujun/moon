<script setup>
// 逻辑留空，但标签必须存在
</script>

<template>
  <!-- 根元素必须有闭合标签 -->
  <div class="doc">
    <!-- 关键：slot 必须写成自闭合形式 -->
    <slot />
  </div>
</template>

<style lang="scss">
/* 全局布局重置 */
html, body {
  margin: 0;
  padding: 0;
  height: 100%;
  background-color: transparent !important;
}

.doc {
  min-height: 100vh;
  background-color: transparent;
  position: relative;
  z-index: 1;
}

/* 暗色遮罩层（可调整透明度） */
.doc::before {
  content: "";
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.6);
  z-index: -1;
  pointer-events: none;
}
</style>
