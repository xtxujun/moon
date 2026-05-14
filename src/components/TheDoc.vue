<style lang="scss">
html, body {
  margin: 0;
  padding: 0;
  height: 100%;
  background-color: transparent !important;
}

.doc {
  min-height: 100vh;
  background-color: transparent;
  position: relative; /* 确保伪元素定位正确 */
  z-index: 1;
}

/* --- 新增代码：暗色遮罩层 --- */
.doc::before {
  content: "";
  position: fixed; /* 固定定位，覆盖整个屏幕 */
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.6); /* 黑色背景，0.6 是透明度 (0-1) */
  z-index: -1; /* 放在内容底下，但在背景图之上（如果背景图是body的话） */
  pointer-events: none; /* 允许鼠标事件穿透，不影响点击 */
}
</style>
