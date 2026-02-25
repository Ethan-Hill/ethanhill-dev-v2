<script>
import { defineAsyncComponent } from 'vue'

const HeroModel = defineAsyncComponent(() => import('./HeroModel.vue'))

export default {
  name: 'HeroSection',
  components: { HeroModel },
  data() {
    return {
      currentRole: 0,
      roles: ['Frontend Developer', 'Vue.js Engineer', 'Design Enthusiast'],
      roleInterval: null,
    }
  },
  computed: {
    displayRole() {
      return this.roles[this.currentRole]
    }
  },
  mounted() {
    this.roleInterval = setInterval(() => {
      this.currentRole = (this.currentRole + 1) % this.roles.length
    }, 3000)
  },
  beforeUnmount() {
    clearInterval(this.roleInterval)
  },
  methods: {
    scrollTo(id) {
      const el = document.getElementById(id)
      if (el) el.scrollIntoView({ behavior: 'smooth' })
    }
  }
}
</script>

<template>
  <section class="relative min-h-screen flex items-center px-6 max-w-6xl mx-auto pt-24 pb-16">
    <div class="w-full grid grid-cols-1 md:grid-cols-2 gap-8 md:gap-16 items-center">

      <!-- Left: text content -->
      <div>
        <h1 class="text-6xl sm:text-7xl md:text-8xl font-light text-[#e8e8e8] leading-[1.05] tracking-tight mb-8">
          Ethan<br />
          <span class="italic font-light text-[#666666]" style="letter-spacing: -0.02em;">Hill</span>
        </h1>

        <div class="flex flex-col gap-4 mb-20">
          <div class="flex items-center gap-3">
            <span class="text-xs text-[#8a8a8a] uppercase tracking-widest">Passion</span>
            <span class="relative overflow-hidden inline-flex" style="min-width: 160px;">
              <Transition name="role">
                <span :key="currentRole" class="text-xs text-[#c8f542] tracking-wide font-medium whitespace-nowrap">
                  {{ displayRole }}
                </span>
              </Transition>
            </span>
          </div>

          <p class="text-base text-[#8a8a8a] max-w-xs leading-relaxed">
            Passionate about building clean, fast web experiences. Currently working full-stack with Vue.js &amp; Laravel at One Utility Bill.
          </p>
        </div>

        <div class="flex items-center gap-8">
          <button
            @click="scrollTo('work')"
            class="inline-flex items-center gap-3 text-sm text-[#e8e8e8] border border-[#1f1f1f] px-6 py-3 hover:border-[#c8f542] hover:text-[#c8f542] transition-all duration-300 group cursor-pointer bg-transparent"
          >
            View Work
            <svg class="w-3.5 h-3.5 group-hover:translate-x-1 transition-transform duration-300" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M17 8l4 4m0 0l-4 4m4-4H3" />
            </svg>
          </button>
          <button
            @click="scrollTo('contact')"
            class="text-sm text-[#8a8a8a] hover:text-[#e8e8e8] transition-colors duration-300 cursor-pointer bg-transparent border-0"
          >
            Get in touch →
          </button>
        </div>
      </div>

      <!-- Right: 3D model — desktop only -->
      <div class="hidden md:block h-[420px]">
        <HeroModel />
      </div>

    </div>

    <!-- Scroll indicator -->
    <button
      @click="scrollTo('work')"
      class="absolute bottom-10 left-1/2 -translate-x-1/2 hidden md:flex flex-col items-center gap-2 bg-transparent border-0 cursor-pointer group"
      aria-label="Scroll to work"
    >
      <span class="text-[10px] text-[#8a8a8a] uppercase tracking-widest group-hover:text-[#c8f542] transition-colors duration-300">Scroll</span>
      <div class="w-px h-12 bg-gradient-to-b from-[#2a2a2a] to-transparent animate-bounce" />
    </button>
  </section>
</template>

<style scoped>
.role-enter-active {
  transition: opacity 0.4s ease, transform 0.4s ease;
}

.role-leave-active {
  transition: opacity 0.4s ease, transform 0.4s ease;
  position: absolute;
}

.role-enter-from {
  opacity: 0;
  transform: translateY(8px);
}

.role-enter-to {
  opacity: 1;
  transform: translateY(0);
}

.role-leave-from {
  opacity: 1;
  transform: translateY(0);
}

.role-leave-to {
  opacity: 0;
  transform: translateY(-8px);
}
</style>