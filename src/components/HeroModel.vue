<script>
import * as THREE from 'three'
import { FontLoader } from 'three/addons/loaders/FontLoader.js'
import { TextGeometry } from 'three/addons/geometries/TextGeometry.js'

export default {
  name: 'HeroModel',
  data() {
    return {
      loading: true,
      mouse: { x: 0, y: 0 },
      lerp: { x: 0, y: 0 },
    }
  },
  mounted() {
    this.init()
    window.addEventListener('mousemove', this.onMouseMove)
  },
  beforeUnmount() {
    window.removeEventListener('mousemove', this.onMouseMove)
    if (this.animFrame) cancelAnimationFrame(this.animFrame)
    if (this.ro) this.ro.disconnect()
    if (this.renderer) this.renderer.dispose()
  },
  methods: {
    onMouseMove(e) {
      this.mouse.x = (e.clientX / window.innerWidth) * 2 - 1
      this.mouse.y = -(e.clientY / window.innerHeight) * 2 + 1
    },

    init() {
      const canvas = this.$refs.canvas
      const w = canvas.clientWidth
      const h = canvas.clientHeight

      // Scene
      this.scene = new THREE.Scene()

      // Camera
      this.camera = new THREE.PerspectiveCamera(42, w / h, 0.1, 100)
      this.camera.position.z = 5.5

      // Renderer — transparent background so it blends with the dark page
      this.renderer = new THREE.WebGLRenderer({ canvas, alpha: true, antialias: true })
      this.renderer.setSize(w, h)
      this.renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2))
      this.renderer.setClearColor(0x000000, 0)

      // Lighting
      const ambient = new THREE.AmbientLight(0xffffff, 0.5)
      this.scene.add(ambient)

      // Key light — slightly warm lime tint
      const keyLight = new THREE.DirectionalLight(0xd8ff70, 3.0)
      keyLight.position.set(4, 4, 6)
      this.scene.add(keyLight)

      // Fill light — cool white from the left
      const fillLight = new THREE.DirectionalLight(0xffffff, 0.7)
      fillLight.position.set(-4, -1, 3)
      this.scene.add(fillLight)

      // Rim light — accent from behind/below
      const rimLight = new THREE.DirectionalLight(0xc8f542, 1.2)
      rimLight.position.set(0, -4, -3)
      this.scene.add(rimLight)

      // Group holds all meshes so we rotate them together
      this.group = new THREE.Group()
      this.scene.add(this.group)

      // Load font and build text geometry
      const loader = new FontLoader()
      loader.load(
        '/helvetiker_bold.typeface.json',
        (font) => {
          const geo = new TextGeometry('EH', {
            font,
            size: 1.1,
            depth: 0.28,
            curveSegments: 10,
            bevelEnabled: true,
            bevelThickness: 0.045,
            bevelSize: 0.028,
            bevelSegments: 6,
          })
          geo.center()

          // Solid lime material
          const mat = new THREE.MeshStandardMaterial({
            color: 0xc8f542,
            metalness: 0.2,
            roughness: 0.18,
          })
          const mesh = new THREE.Mesh(geo, mat)
          this.group.add(mesh)

          // Very subtle wireframe overlay adds depth
          const wireMat = new THREE.MeshBasicMaterial({
            color: 0xffffff,
            wireframe: true,
            transparent: true,
            opacity: 0.04,
          })
          this.group.add(new THREE.Mesh(geo.clone(), wireMat))

          this.loading = false
        },
        undefined,
        (err) => {
          console.error('Three.js font failed to load', err)
          this.loading = false
        }
      )

      // Keep canvas crisp on resize
      this.ro = new ResizeObserver(() => {
        const canvas = this.$refs.canvas
        if (!canvas) return
        const w = canvas.clientWidth
        const h = canvas.clientHeight
        this.camera.aspect = w / h
        this.camera.updateProjectionMatrix()
        this.renderer.setSize(w, h)
      })
      this.ro.observe(canvas)

      this.animate()
    },

    animate() {
      this.animFrame = requestAnimationFrame(this.animate)
      const t = performance.now() * 0.001

      // Smooth lerp toward real mouse position
      const speed = 0.055
      this.lerp.x += (this.mouse.x - this.lerp.x) * speed
      this.lerp.y += (this.mouse.y - this.lerp.y) * speed

      if (this.group) {
        // Rotate to face cursor
        this.group.rotation.y = this.lerp.x * 0.45
        this.group.rotation.x = -this.lerp.y * 0.3

        // Gentle floating bob
        this.group.position.y = Math.sin(t * 0.9) * 0.07
      }

      this.renderer.render(this.scene, this.camera)
    },
  },
}
</script>

<template>
  <div class="relative w-full h-full">
    <canvas ref="canvas" class="w-full h-full" />

    <!-- Spinner while font loads -->
    <Transition name="fade">
      <div v-if="loading" class="absolute inset-0 flex items-center justify-center">
        <div class="w-5 h-5 border border-[#2a2a2a] border-t-[#c8f542] rounded-full animate-spin" />
      </div>
    </Transition>
  </div>
</template>

<style scoped>
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s ease;
}
.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>
