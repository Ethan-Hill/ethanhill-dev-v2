<script>
function getDuration(startYear, startMonth) {
  const now = new Date()
  const start = new Date(startYear, startMonth - 1, 1)
  let years = now.getFullYear() - start.getFullYear()
  let months = now.getMonth() - start.getMonth()
  if (months < 0) {
    years--
    months += 12
  }
  const parts = []
  if (years > 0) parts.push(`${years} yr${years !== 1 ? 's' : ''}`)
  if (months > 0) parts.push(`${months} mo${months !== 1 ? 's' : ''}`)
  return parts.join(' ') + ' · Current'
}

export default {
  name: 'AboutSection',
  data() {
    return {
      bioOne: `I'm Ethan Hill — a passionate Frontend Developer, currently 22. I started my programming journey in 2017 when I was first introduced to HTML, and since then I've been working to build a career in Software Engineering and Web Development.`,
      bioTwo: `I spend a lot of my spare time creating projects to help myself learn new aspects of different programming languages and design methodologies. I've been studying software engineering and web development since 2019 and it has been awesome.`,
      skills: ['Vue.js', 'Nuxt 3', 'TypeScript', 'TailwindCSS', 'Pinia', 'Laravel', 'Git', 'Figma', 'Node.js'],
      timeline: [
        {
          period: 'High School',
          dates: '3 Years',
          place: 'Whitley Bay High School',
          detail: 'Studied Design and Technology with Systems — programming circuit boards, building a speaker with a 3.5mm audio jack and working lights, all synced.'
        },
        {
          period: 'College',
          dates: '3 Years',
          place: 'Gateshead College',
          detail: 'Studied Software Engineering and Development. Near the end I picked up HTML, CSS and JavaScript — got completely hooked on web development and never looked back.'
        },
        {
          period: 'Work',
          dates: '2 Years',
          place: 'Drummond Central',
          detail: 'Worked as a Frontend Developer in an agency environment, collaborating with brands like END, Nando\'s, and Greggs. Focused on building systems to make frontend development faster and more consistent for the team.'
        },
        {
          period: 'Work',
          dates: getDuration(2023, 6),
          place: 'One Utility Bill',
          detail: 'Working as a Full Stack Developer using Vue.js and Laravel in a hybrid environment. Building and maintaining web applications while collaborating with teams in Newcastle Upon Tyne.'
        },
      ]
    }
  }
}
</script>

<template>
  <section id="about" class="px-6 max-w-6xl mx-auto py-32">
    <div class="border-t border-[#1f1f1f] pt-16">

      <!-- Header -->
      <div class="mb-20">
        <span class="text-xs text-[#8a8a8a] uppercase tracking-widest block mb-2">About</span>
        <h2 class="text-3xl font-light text-[#e8e8e8] tracking-tight">Background</h2>
      </div>

      <div class="grid grid-cols-1 md:grid-cols-2 gap-16 md:gap-24">

        <!-- Bio + skills -->
        <div>
          <p class="text-sm text-[#8a8a8a] leading-relaxed mb-4">
            {{ bioOne }}
          </p>
          <p class="text-sm text-[#8a8a8a] leading-relaxed mb-10">
            {{ bioTwo }}
          </p>

          <!-- Skills -->
          <div>
            <span class="text-[10px] uppercase tracking-widest text-[#8a8a8a] block mb-4">Technologies</span>
            <div class="flex flex-wrap gap-2">
              <span
                v-for="skill in skills"
                :key="skill"
                class="text-xs text-[#888888] border border-[#1f1f1f] px-3 py-1.5 hover:border-[#c8f542] hover:text-[#c8f542] transition-all duration-300"
              >
                {{ skill }}
              </span>
            </div>
          </div>
        </div>

        <!-- Timeline -->
        <div>
          <span class="text-[10px] uppercase tracking-widest text-[#8a8a8a] block mb-6">Timeline</span>
          <div class="relative">
            <!-- Vertical line -->
            <div class="absolute left-0 top-2 bottom-2 w-px bg-[#1f1f1f]" />

            <div class="space-y-10 pl-6">
              <div
                v-for="(item, i) in timeline"
                :key="i"
                class="relative"
              >
                <!-- Dot -->
                <div class="absolute -left-[25px] top-1.5 w-1.5 h-1.5 rounded-full border border-[#2a2a2a] bg-[#0a0a0a]" />

                <span class="text-[10px] uppercase tracking-widest text-[#8a8a8a] block mb-1">{{ item.period }}</span>
                <p class="text-sm font-medium text-[#e8e8e8] mb-0.5">{{ item.place }}</p>
                <p class="text-xs text-[#8a8a8a] mb-2">{{ item.dates }}</p>
                <p class="text-xs text-[#8a8a8a] leading-relaxed">{{ item.detail }}</p>
              </div>
            </div>
          </div>
        </div>

      </div>
    </div>
  </section>
</template>
