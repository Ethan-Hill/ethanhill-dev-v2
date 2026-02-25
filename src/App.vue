<script>
import NavBar from './components/NavBar.vue'
import HeroSection from './components/HeroSection.vue'
import WorkSection from './components/WorkSection.vue'
import AboutSection from './components/AboutSection.vue'
import ContactSection from './components/ContactSection.vue'
import SiteFooter from './components/SiteFooter.vue'
import CustomCursor from './components/CustomCursor.vue'

export default {
  name: 'App',
  components: {
    NavBar,
    HeroSection,
    WorkSection,
    AboutSection,
    ContactSection,
    SiteFooter,
    CustomCursor
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
  </div>
</template>
