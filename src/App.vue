<template>
  <div class="main-container">
    <header class="top-bar">
      <button
        id="mobile-menu"
        class="mobile-menu"
        @click="handleShowMenu"
      ></button>
      <h1 class="logo">
        <a href="/"><img src="./assets/images/logo.svg" alt="Room" /></a>
      </h1>
      <nav :class="['navbar', { show: showNavBar }]">
        <button
          id="mobile-menu-close"
          class="mobile-menu close"
          @click="handleShowMenu"
        ></button>
        <ul class="nav-list">
          <li><a href="#">home</a></li>
          <li><a href="#">shop</a></li>
          <li><a href="#">about</a></li>
          <li><a href="#">contact</a></li>
        </ul>
      </nav>
    </header>
    <div class="hero">
      <div class="img-container">
        <div
          v-for="(slide, index) in slides"
          :key="slide.id"
          class="slide-wrapper"
        >
          <transition :name="direction">
            <slide v-show="index === counter" :slide="slide" />
          </transition>
        </div>
      </div>
      <div class="desc-container">
        <transition name="door">
          <slide-desc :slide="currentSlide" :key="currentSlide.id" />
        </transition>
      </div>
      <div class="carousel-nav">
        <button id="nav-btn-left" @click="goLeft" class="left">
          <img src="./assets/images/icon-angle-left.svg" alt="" />
        </button>
        <button id="nav-btn-right" @click="goRight" class="right">
          <img src="./assets/images/icon-angle-right.svg" alt="" />
        </button>
      </div>
    </div>
    <div class="about">
      <div class="about-img about-img-left"></div>
      <div class="about-desc">
        <h3>About our furniture</h3>
        <p>
          Our multifunctional collection blends design and function to suit your
          individual taste. Make each room unique, or pick a cohesive theme that
          best express your interests and what inspires you. Find the furniture
          pieces you need, from traditional to contemporary styles or anything
          in between. Product specialists ara available to help you create your
          dream space.
        </p>
      </div>
      <div class="about-img about-img-right"></div>
    </div>
  </div>
</template>

<script setup>
  import Slide from './components/Slide.vue'
  import SlideDesc from './components/SlideDesc.vue'
  import { ref, computed, onMounted, onUnmounted } from 'vue'
  import deskImg1 from './assets/images/desktop-image-hero-1.jpg'
  import deskImg2 from './assets/images/desktop-image-hero-2.jpg'
  import deskImg3 from './assets/images/desktop-image-hero-3.jpg'
  import mobImg1 from './assets/images/mobile-image-hero-1.jpg'
  import mobImg2 from './assets/images/mobile-image-hero-2.jpg'
  import mobImg3 from './assets/images/mobile-image-hero-3.jpg'
  const showNavBar = ref(false)
  const counter = ref(0)
  const direction = ref('right')
  const slides = ref([
    {
      id: 1,
      title: 'Discover innovative ways to decorate',
      desc: 'We provide unmatched quality, comfort, and style for property owners across the country. Our experts combine form and function in bringing your vision to life. Create a room in your own style with our collection and make your property a reflection of you and what you love.',

      deskImgUrl: deskImg1,
      mobImgUrl: mobImg1,
      alt: 'Dinner Table',
    },
    {
      id: 2,
      title: 'We are available al across the globe',
      desc: 'With stores all over the world, it’s easy for you to find furniture for your home or place of business. Locally, we’re in most major cities throughout the country. Find the branch nearest you using our store locator. Any questions? Don’t hesitate to contact us today.',
      deskImgUrl: deskImg2,
      mobImgUrl: mobImg2,
      alt: '3 chairs',
    },
    {
      id: 3,
      title: 'Manufactured with the best materials',
      desc: 'Our modem furniture store provide a high level of quality. Our company has invested in advanced technology to ensure that every product is made as perfect and as consistent as possible. With three decades of experience in this industry, we understand what customers want for their home and office.',
      deskImgUrl: deskImg3,
      mobImgUrl: mobImg3,
      alt: 'black chair',
    },
  ])

  const currentSlide = computed(() => {
    return slides.value[counter.value]
  })

  const goLeft = () => {
    if (counter.value === 0) {
      counter.value = 2
    } else {
      counter.value--
    }
    direction.value = 'right'
  }
  const goRight = () => {
    if (counter.value === 2) {
      counter.value = 0
    } else {
      counter.value++
    }
    direction.value = 'left'
  }
  const handleNavonKeys = (e) => {
    if (e.key === 'ArrowRight') {
      goRight()
    } else if (e.key === 'ArrowLeft') {
      goLeft()
    }
    return
  }
  const handleShowMenu = () => {
    showNavBar.value = !showNavBar.value
    const body = document.getElementsByTagName('body')[0]
    const mainContainer = document.querySelector('.main-container')

    if (showNavBar.value) {
      body.style.position = 'fixed'
      mainContainer.classList.add('overlay')
    } else {
      body.style.position = 'relative'
      mainContainer.classList.remove('overlay')
    }
  }
  onMounted(() => {
    document.addEventListener('keydown', handleNavonKeys)
  })
  onUnmounted(() => {
    document.removeEventListener('keydown', handleNavonKeys)
  })
</script>
<style lang="scss"></style>
