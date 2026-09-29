<template>
  <div class="pdf-page-counter">
    <SlideCurrentNo /> / <SlidesTotal />
  </div>
</template>

<style scoped>
.pdf-page-counter {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  min-width: 3.2rem;
  padding: 0.34rem 0.55rem;
  border: 1px solid #d9e3ea;
  border-radius: 5px;
  background: rgba(255, 255, 255, 0.94);
  box-shadow: 0 8px 18px rgba(15, 76, 129, 0.08);
  color: #08385f;
  font-size: 0.72rem;
  font-weight: 700;
  line-height: 1;
}
</style>