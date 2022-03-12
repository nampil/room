<template>
  <div ref="imgSlideContent" class="img-slide-content"></div>
  <!-- <picture>
    <source
      media="(max-width: 375px)"
      width="375"
      height="360"
      :srcset="props.slide.mobImgUrl"
    />
    <source
      media="(min-width: 376px)"
      width="840"
      height="534"
      :srcset="props.slide.deskImgUrl"
    />
    <img :src="props.slide.deskImgUrl" alt="" />
  </picture> -->
</template>

<script setup>
  import { onMounted, ref } from 'vue'

  const props = defineProps(['slide'])
  const imgSlideContent = ref(null)
  onMounted(() => {
    imgSlideContent.value.style.setProperty(
      '--bg-image-mobile',
      `url(.${props.slide.mobImgUrl})`
    )
    imgSlideContent.value.style.setProperty(
      '--bg-image-desk',
      `url(.${props.slide.deskImgUrl})`
    )
  })
</script>

<style lang="scss" scoped>
  picture {
    height: 100%;
  }
  img {
    width: 100%;
    height: 100%;
    -o-object-fit: cover;
    object-fit: cover;
  }
</style>
