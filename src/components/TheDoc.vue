<script setup>
// 可以留空，但标签要存在
</script>

<template>
  <!-- 注意：这里必须有一个根元素包裹内容 -->
  <div class="doc">
    <!-- <slot /> 表示这里会插入 index.vue 里的内容 -->
    <slot />
  </div>
</template>

<style lang="scss">
/* 让 html 和 body 高度占满屏幕，且无默认边距 */
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

/* --- 新增代码：暗色遮罩层 --- */
.doc::before {
  content: "";
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.6); /* 黑色半透明，可根据喜好调整 0.6 */
  z-index
