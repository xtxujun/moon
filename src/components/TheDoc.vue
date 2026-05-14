<script setup>
</script>

<template>
  <div class="doc">
    <slot />
  </div>
</template>

<style lang="scss"> /* 注意这里去掉了 scoped */
html, body {
  margin: 0;
  padding: 0;
  height: 100%;
  background-color: transparent !important;
}

.doc {
  min-height: 100vh;
  background-color: transparent;
}
</style>
