<script setup>
// 逻辑留空
</script>

<template>
  <div class="doc">
    <slot />
  </div>
</template>

<style lang="scss" scoped>
/* 确保 html/body 透明，让 App.vue 的背景透出来 */
html, body {
  margin: 0;
  padding: 0;
  height: 100%;
  background-color: transparent !important;
  overflow: hidden; /* 防止滚动条干扰 */
}

.doc {
  /* 关键样式：透明白色磨砂 */
  
  /* 1. 背景色：rgba(红, 绿, 蓝, 透明度) -> 0.65 是透明度，你可以调 */
  background-color: rgba(255, 255, 255, 0.65);
  
  /* 2. 磨砂模糊：数值越大越模糊 */
  backdrop-filter: blur(12px);
  -webkit-backdrop-filter: blur(12px); /* 兼容 Safari */
  
  /* 3. 布局设置 */
  min-height: 100vh;
  width: 100%;
  position: relative;
  box-sizing: border-box;
  
  /* 可选：加一点边框让它更有质感 */
  /* border: 1px solid rgba(255, 255, 255, 0.3); */
}
</style>
