<script>
export default {
  name: 'SiteFooter',
  data() {
    return {
      year: new Date().getFullYear()
    }
  }
}
</script>

<template>
  <footer class="px-6 max-w-6xl mx-auto py-10 border-t border-[#1f1f1f] flex items-center justify-between">
    <span class="text-xs text-[#8a8a8a]">© {{ year }} Ethan Hill</span>
    <span class="text-xs text-[#8a8a8a]">Built with Vue 3 — Options API</span>
  </footer>
</template>
