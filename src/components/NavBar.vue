<script>
export default {
  name: 'NavBar',
  data() {
    return {
      scrolled: false,
      menuOpen: false,
      links: [
        { label: 'Work', id: 'work' },
        { label: 'About', id: 'about' },
        { label: 'Contact', id: 'contact' },
      ]
    }
  },
  mounted() {
    window.addEventListener('scroll', this.onScroll)
  },
  beforeUnmount() {
    window.removeEventListener('scroll', this.onScroll)
  },
  methods: {
    onScroll() {
      this.scrolled = window.scrollY > 40
    },
    scrollTo(id) {
      const el = document.getElementById(id)
      if (el) el.scrollIntoView({ behavior: 'smooth' })
      this.menuOpen = false
    }
  }
}
</script>

<template>
  <header
    class="fixed top-0 left-0 right-0 z-50 transition-all duration-500"
    :class="scrolled ? 'bg-[#0a0a0a]/90 backdrop-blur-md border-b border-[#1f1f1f]' : ''"
  >
    <nav class="max-w-6xl mx-auto flex items-center justify-between px-6 py-5">
      <a href="#" class="text-sm font-medium tracking-widest uppercase text-[#e8e8e8] hover:text-[#c8f542] transition-colors duration-300">
        Ethan Hill
      </a>

      <!-- Desktop -->
      <ul class="hidden md:flex items-center gap-10">
        <li v-for="link in links" :key="link.id">
          <button
            @click="scrollTo(link.id)"
            class="text-sm text-[#8a8a8a] hover:text-[#e8e8e8] transition-colors duration-300 tracking-wide bg-transparent border-0 cursor-pointer"
          >
            {{ link.label }}
          </button>
        </li>
      </ul>

      <!-- Mobile toggle -->
      <button
        class="md:hidden flex flex-col gap-1.5 p-1"
        @click="menuOpen = !menuOpen"
        aria-label="Toggle menu"
      >
        <span class="block w-5 h-px bg-[#e8e8e8] transition-all duration-300" :class="menuOpen ? 'rotate-45 translate-y-2' : ''" />
        <span class="block w-5 h-px bg-[#e8e8e8] transition-all duration-300" :class="menuOpen ? 'opacity-0' : ''" />
        <span class="block w-5 h-px bg-[#e8e8e8] transition-all duration-300" :class="menuOpen ? '-rotate-45 -translate-y-2' : ''" />
      </button>
    </nav>

    <!-- Mobile menu -->
    <div
      class="md:hidden overflow-hidden transition-all duration-300 border-t border-[#1f1f1f]"
      :class="menuOpen ? 'max-h-48' : 'max-h-0'"
    >
      <ul class="flex flex-col px-6 py-4 gap-4">
        <li v-for="link in links" :key="link.id">
          <button
            @click="scrollTo(link.id)"
            class="text-sm text-[#8a8a8a] hover:text-[#e8e8e8] transition-colors duration-300 bg-transparent border-0 cursor-pointer w-full text-left"
          >
            {{ link.label }}
          </button>
        </li>
      </ul>
    </div>
  </header>
</template>
