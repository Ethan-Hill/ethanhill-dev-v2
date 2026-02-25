<script>
import { ref, onMounted, onUnmounted } from 'vue'

export default {
  name: 'CustomCursor',
  setup() {
    const x = ref(0)
    const y = ref(0)
    const isHovering = ref(false)
    const isVisible = ref(false)

    const updateCursor = (e) => {
      x.value = e.clientX
      y.value = e.clientY
      if (!isVisible.value) isVisible.value = true
    }

    const handleMouseOver = (e) => {
      const target = e.target
      const isInteractive = target.closest('a, button, [role="button"]')
      if (isInteractive) {
        isHovering.value = true
      }
    }

    const handleMouseOut = (e) => {
      const target = e.target
      const isInteractive = target.closest('a, button, [role="button"]')
      if (isInteractive) {
        isHovering.value = false
      }
    }

    onMounted(() => {
      window.addEventListener('mousemove', updateCursor)
      window.addEventListener('mouseover', handleMouseOver)
      window.addEventListener('mouseout', handleMouseOut)
    })

    onUnmounted(() => {
      window.removeEventListener('mousemove', updateCursor)
      window.removeEventListener('mouseover', handleMouseOver)
      window.removeEventListener('mouseout', handleMouseOut)
    })

    return { x, y, isHovering, isVisible }
  }
}
</script>

<template>
  <div 
    class="custom-cursor"
    :class="{ 'is-hovering': isHovering, 'is-visible': isVisible }"
    :style="{ transform: `translate3d(${x}px, ${y}px, 0)` }"
  >
    <div class="cursor-inner"></div>
  </div>
</template>

<style scoped>
.custom-cursor {
  position: fixed;
  top: 0;
  left: 0;
  width: 24px;
  height: 24px;
  margin-top: -12px;
  margin-left: -12px;
  pointer-events: none;
  z-index: 10000;
  opacity: 0;
  transition: opacity 0.5s cubic-bezier(0.16, 1, 0.3, 1), transform 0.15s cubic-bezier(0.23, 1, 0.32, 1);
  will-change: transform;
}

.custom-cursor.is-visible {
  opacity: 1;
}

.cursor-inner {
  width: 100%;
  height: 100%;
  border: 1.5px solid rgba(255, 255, 255, 0.4);
  border-radius: 50%;
  transition: all 0.4s cubic-bezier(0.16, 1, 0.3, 1);
  box-shadow: 0 0 15px rgba(255, 255, 255, 0.1);
}

.custom-cursor.is-hovering .cursor-inner {
  transform: scale(2.5);
  background: rgba(255, 255, 255, 0.1);
  border-color: rgba(255, 255, 255, 0.9);
  box-shadow: 0 0 25px rgba(255, 255, 255, 0.3);
}

/* Hide default cursor globally if we want a full replacement */
:global(*) {
  cursor: none !important;
}

@media (max-width: 768px) {
  .custom-cursor {
    display: none;
  }
  :global(*) {
    cursor: auto !important;
  }
}
</style>
