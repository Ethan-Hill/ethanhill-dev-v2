<script>
export default {
  name: 'ContactSection',
  data() {
    return {
      socials: [
        { label: 'GitHub', href: 'https://github.com/Ethan-Hill', icon: 'github' },
        { label: 'Twitter', href: 'https://x.com/EthanJayHill', icon: 'twitter' },
        { label: 'LinkedIn', href: 'https://www.linkedin.com/in/ethanjayhill/', icon: 'linkedin' },
      ]
    }
  }
}
</script>

<template>
  <section id="contact" class="px-6 max-w-6xl mx-auto py-32">
    <div class="border-t border-[#1f1f1f] pt-16">

      <div class="max-w-xl">
        <span class="text-xs text-[#8a8a8a] uppercase tracking-widest block mb-2">Contact</span>
        <h2 class="text-3xl font-light text-[#e8e8e8] tracking-tight mb-6">Let's work together.</h2>
        <p class="text-sm text-[#8a8a8a] leading-relaxed mb-10">
         If you have something interesting, I'd love to hear about it.
        </p>

        <div class="flex items-center gap-6">
          <!-- GitHub -->
          <a href="https://github.com/Ethan-Hill" class="text-[#4a4a4a] hover:text-[#c8f542] transition-colors duration-300" target="_blank" rel="noopener" aria-label="GitHub">
            <svg class="w-5 h-5" fill="currentColor" viewBox="0 0 24 24">
              <path d="M12 0a12 12 0 00-3.793 23.4c.6.111.82-.261.82-.58 0-.286-.011-1.243-.016-2.252-3.338.726-4.042-1.608-4.042-1.608-.546-1.388-1.333-1.757-1.333-1.757-1.09-.744.082-.729.082-.729 1.205.085 1.839 1.237 1.839 1.237 1.07 1.834 2.807 1.304 3.492.997.108-.775.418-1.305.762-1.605-2.665-.303-5.466-1.332-5.466-5.931 0-1.31.468-2.381 1.236-3.221-.124-.304-.535-1.524.117-3.176 0 0 1.008-.322 3.301 1.23A11.51 11.51 0 0112 5.803c1.02.005 2.047.138 3.006.404 2.29-1.552 3.297-1.23 3.297-1.23.653 1.653.242 2.874.118 3.176.769.84 1.235 1.911 1.235 3.221 0 4.61-2.805 5.625-5.475 5.922.43.372.823 1.102.823 2.222 0 1.606-.015 2.898-.015 3.293 0 .321.217.695.825.578A12.001 12.001 0 0012 0z"/>
            </svg>
          </a>
          <!-- Twitter/X -->
          <a href="https://x.com/EthanJayHill" class="text-[#4a4a4a] hover:text-[#c8f542] transition-colors duration-300" target="_blank" rel="noopener" aria-label="Twitter">
            <svg class="w-5 h-5" fill="currentColor" viewBox="0 0 24 24">
              <path d="M18.244 2.25h3.308l-7.227 8.26 8.502 11.24H16.17l-5.214-6.817L4.99 21.75H1.68l7.73-8.835L1.254 2.25H8.08l4.713 6.231zm-1.161 17.52h1.833L7.084 4.126H5.117z"/>
            </svg>
          </a>
          <!-- LinkedIn -->
          <a href="https://www.linkedin.com/in/ethanjayhill/" class="text-[#4a4a4a] hover:text-[#c8f542] transition-colors duration-300" target="_blank" rel="noopener" aria-label="LinkedIn">
            <svg class="w-5 h-5" fill="currentColor" viewBox="0 0 24 24">
              <path d="M20.447 20.452h-3.554v-5.569c0-1.328-.027-3.037-1.852-3.037-1.853 0-2.136 1.445-2.136 2.939v5.667H9.351V9h3.414v1.561h.046c.477-.9 1.637-1.85 3.37-1.85 3.601 0 4.267 2.37 4.267 5.455v6.286zM5.337 7.433a2.062 2.062 0 01-2.063-2.065 2.064 2.064 0 112.063 2.065zm1.782 13.019H3.555V9h3.564v11.452zM22.225 0H1.771C.792 0 0 .774 0 1.729v20.542C0 23.227.792 24 1.771 24h20.451C23.2 24 24 23.227 24 22.271V1.729C24 .774 23.2 0 22.222 0h.003z"/>
            </svg>
          </a>
        </div>
      </div>

    </div>
  </section>
</template>
