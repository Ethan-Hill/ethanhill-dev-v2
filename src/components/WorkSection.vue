<script>
export default {
  name: 'WorkSection',
  data() {
    return {
      projects: [
        {
          id: 5,
          title: 'JibberJab',
          year: '2026',
          tags: ['Laravel', 'Vue 3', 'Vite', 'Pusher', 'TailwindCSS'],
          description: 'A modern, real-time social platform (Twitter clone) featuring real-time messaging, dynamic feeds, and a sleek, responsive interface.',
          repo: 'https://github.com/Ethan-Hill/JibberJab',
        },
        {
          id: 4,
          title: 'ethanhill.dev (v2)',
          year: '2026',
          tags: ['Vue 3', 'Three.js', 'Vite', 'TailwindCSS'],
          description: 'The second iteration of my personal portfolio, focusing on performance, smooth animations, and a refined aesthetic using Vue 3 and Three.js.',
          repo: 'https://github.com/Ethan-Hill/ethanhill-dev-v2',
        },
        {
          id: 1,
          title: 'TeeDee',
          year: '2024',
          tags: ['Nuxt 3', 'TailwindCSS', 'Supabase', 'GitHub OAuth'],
          description: 'A simple todo app built with Nuxt 3. Users log in with their GitHub account and can create, complete, and remove tasks — all stored in a Supabase database.',
          repo: 'https://github.com/Ethan-Hill/TeeDee',
        },
        {
          id: 2,
          title: 'Nuxify',
          year: '2023',
          tags: ['Nuxt 2', 'Spotify API'],
          description: 'My first Nuxt web app, integrating with the Spotify Web API. Login, control playback, and search your playlists and songs.',
          repo: 'https://github.com/Ethan-Hill/Nuxify',
        },
        {
          id: 3,
          title: 'Webify',
          year: '2023',
          tags: ['Next.js', 'TypeScript', 'Spotify API'],
          description: 'A Next.js & TypeScript web app integrating with the Spotify Web API to view your profile, playlists, and listening stats.',
          repo: 'https://github.com/Ethan-Hill/Webify',
        },
      ]
    }
  }
}
</script>

<template>
  <section id="work" class="px-6 max-w-6xl mx-auto py-32">
    <!-- Section header -->
    <div class="flex items-center justify-between mb-16">
      <div>
        <span class="text-xs text-[#8a8a8a] uppercase tracking-widest block mb-2">Selected Work</span>
        <h2 class="text-3xl font-light text-[#e8e8e8] tracking-tight">Projects</h2>
      </div>
      <span class="text-xs text-[#8a8a8a] tabular-nums">0{{ projects.length }}</span>
    </div>

    <!-- Project list -->
    <div class="divide-y divide-[#1f1f1f]">
      <article
        v-for="(project, index) in projects"
        :key="project.id"
        class="group py-8 grid grid-cols-12 gap-4 items-start hover:bg-[#111111] transition-colors duration-300 -mx-4 px-4"
      >
        <!-- Index -->
        <span class="col-span-1 text-xs text-[#8a8a8a] tabular-nums pt-1">{{ String(index + 1).padStart(2, '0') }}</span>

        <!-- Title + tags -->
        <div class="col-span-12 sm:col-span-4">
          <h3 class="text-lg font-medium text-[#e8e8e8] group-hover:text-[#c8f542] transition-colors duration-300 mb-2">
            {{ project.title }}
          </h3>
          <div class="flex flex-wrap gap-1.5">
            <span
              v-for="tag in project.tags"
              :key="tag"
              class="text-[10px] uppercase tracking-widest text-[#888888] border border-[#1f1f1f] px-2 py-0.5"
            >
              {{ tag }}
            </span>
          </div>
        </div>

        <!-- Description -->
        <p class="col-span-12 sm:col-span-5 text-sm text-[#8a8a8a] leading-relaxed">
          {{ project.description }}
        </p>

        <!-- Year + links -->
        <div class="col-span-12 sm:col-span-2 flex sm:flex-col items-center sm:items-end gap-4">
          <span class="text-xs text-[#8a8a8a] tabular-nums">{{ project.year }}</span>
          <div class="flex gap-3">
            <a v-if="project.repo" :href="project.repo" class="text-[#8a8a8a] hover:text-[#c8f542] transition-colors duration-300" aria-label="GitHub repo" target="_blank" rel="noopener">
              <svg class="w-4 h-4" fill="currentColor" viewBox="0 0 24 24">
                <path d="M12 0a12 12 0 00-3.793 23.4c.6.111.82-.261.82-.58 0-.286-.011-1.243-.016-2.252-3.338.726-4.042-1.608-4.042-1.608-.546-1.388-1.333-1.757-1.333-1.757-1.09-.744.082-.729.082-.729 1.205.085 1.839 1.237 1.839 1.237 1.07 1.834 2.807 1.304 3.492.997.108-.775.418-1.305.762-1.605-2.665-.303-5.466-1.332-5.466-5.931 0-1.31.468-2.381 1.236-3.221-.124-.304-.535-1.524.117-3.176 0 0 1.008-.322 3.301 1.23A11.51 11.51 0 0112 5.803c1.02.005 2.047.138 3.006.404 2.29-1.552 3.297-1.23 3.297-1.23.653 1.653.242 2.874.118 3.176.769.84 1.235 1.911 1.235 3.221 0 4.61-2.805 5.625-5.475 5.922.43.372.823 1.102.823 2.222 0 1.606-.015 2.898-.015 3.293 0 .321.217.695.825.578A12.001 12.001 0 0012 0z"/>
              </svg>
            </a>
            <a v-if="project.link" :href="project.link" class="text-[#8a8a8a] hover:text-[#c8f542] transition-colors duration-300" aria-label="Live link" target="_blank" rel="noopener">
              <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10 6H6a2 2 0 00-2 2v10a2 2 0 002 2h10a2 2 0 002-2v-4M14 4h6m0 0v6m0-6L10 14" />
              </svg>
            </a>
          </div>
        </div>
      </article>
    </div>
  </section>
</template>
