<script>
import { ref, onMounted, onUnmounted } from 'vue'

export default {
  name: 'ScrollToTop',
  setup() {
    const isVisible = ref(false)

    const checkScroll = () => {
      // Calculate how far the user has scrolled
      const scrollY = window.scrollY
      const windowHeight = window.innerHeight
      const documentHeight = document.documentElement.scrollHeight

      // Show the button if the user is near the bottom of the page (within 200px)
      // or if they have scrolled a significant amount down
      if (scrollY + windowHeight >= documentHeight - 500) {
        isVisible.value = true
      } else {
        isVisible.value = false
      }
    }

    const scrollToTop = () => {
      window.scrollTo({
        top: 0,
        behavior: 'smooth'
      })
    }

    onMounted(() => {
      window.addEventListener('scroll', checkScroll, { passive: true })
      checkScroll()
    })

    onUnmounted(() => {
      window.removeEventListener('scroll', checkScroll)
    })

    return { isVisible, scrollToTop }
  }
}
</script>

<template>
  <Transition name="fade-slide">
    <button
      v-if="isVisible"
      @click="scrollToTop"
      class="fixed bottom-8 right-8 z-40 p-3 bg-[#111111] border border-[#1f1f1f] text-[#8a8a8a] hover:text-[#c8f542] hover:border-[#c8f542] transition-colors duration-300 rounded-full cursor-pointer shadow-lg flex items-center justify-center group"
      aria-label="Scroll to top"
    >
      <svg class="w-5 h-5 group-hover:-translate-y-1 transition-transform duration-300" fill="none" stroke="currentColor" viewBox="0 0 24 24">
        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M5 10l7-7m0 0l7 7m-7-7v18" />
      </svg>
    </button>
  </Transition>
</template>

<style scoped>
.fade-slide-enter-active,
.fade-slide-leave-active {
  transition: opacity 0.4s ease, transform 0.4s ease;
}

.fade-slide-enter-from,
.fade-slide-leave-to {
  opacity: 0;
  transform: translateY(20px);
}
</style>
