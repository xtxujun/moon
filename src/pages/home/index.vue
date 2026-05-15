<style lang="scss" scoped>
/* ==================== 明亮模式文字对比度优化 ==================== */
.group__name,
.site-name,
.text,
span {
  color: #1f2937 !important;        /* 深黑色，提升明亮模式清晰度 */
  font-weight: 500;
}

/* 暗黑模式保持亮白色 */
.dark .group__name,
.dark .site-name,
.dark span {
  color: #f1f5f9 !important;
}

/* 图标卡片文字悬停效果 */
.SiteItemCard {
  transition: all 0.2s ease;
}

.SiteItemCard:hover {
  transform: translateY(-3px);
  filter: drop-shadow(0 10px 20px rgba(0, 0, 0, 0.15));
}

/* 原有样式保留 + 轻微增强 */
.site--setting {
  border: 1px dashed var(--setting-border-c);
}

.group__name {
  position: relative;
  &::before {
    content: '';
    width: 4px;
    height: 72%;
    position: absolute;
    left: 0;
    top: 50%;
    transform: translateY(-50%);
    background: var(--primary-c);
    border-radius: 2px;
  }
}

.group__header--setting {
  border: 1px dashed var(--setting-border-c);
}

.btn--add-site {
  box-shadow: rgba(60, 64, 67, 0.3) 0px 1px 2px 0px, rgba(60, 64, 67, 0.15) 0px 1px 3px 1px;
}
</style>
