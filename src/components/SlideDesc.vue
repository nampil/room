<template>
  <div class="slide-desc">
    <h2>{{ props.slide.title }}</h2>
    <p>
      {{ props.slide.desc }}
    </p>
    <a class="shop-now-btn" href="#"
      >SHOP NOW <span><img src="../assets/images/icon-arrow.svg" alt="" /></span
    ></a>
  </div>
</template>

<script setup>
  const props = defineProps(['slide'])
</script>

<style lang="scss" scoped></style>
