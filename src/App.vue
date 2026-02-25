<script>
import { defineAsyncComponent } from 'vue'
import NavBar from './components/NavBar.vue'
import HeroSection from './components/HeroSection.vue'
import CustomCursor from './components/CustomCursor.vue'

const WorkSection = defineAsyncComponent(() => import('./components/WorkSection.vue'))
const AboutSection = defineAsyncComponent(() => import('./components/AboutSection.vue'))
const ContactSection = defineAsyncComponent(() => import('./components/ContactSection.vue'))
const SiteFooter = defineAsyncComponent(() => import('./components/SiteFooter.vue'))
const ScrollToTop = defineAsyncComponent(() => import('./components/ScrollToTop.vue'))

export default {
  name: 'App',
  components: {
    NavBar,
    HeroSection,
    WorkSection,
    AboutSection,
    ContactSection,
    SiteFooter,
    CustomCursor,
    ScrollToTop
  }
}
</script>

<template>
  <div class="min-h-screen bg-[#0a0a0a] text-[#e8e8e8]">
    <NavBar />
    <main>
      <HeroSection />
      <WorkSection />
      <AboutSection />
      <ContactSection />
    </main>
    <SiteFooter />
    <CustomCursor />
    <ScrollToTop />
  </div>
</template>
