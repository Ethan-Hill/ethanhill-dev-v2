<script>
import { ref, onMounted, onUnmounted } from 'vue'

export default {
  name: 'CustomCursor',
  setup() {
    const isHovering = ref(false)
    const isVisible = ref(false)
    const cursorRef = ref(null)
    
    let rafId = null
    let mouseX = 0
    let mouseY = 0

    const moveCursor = () => {
      if (cursorRef.value) {
        cursorRef.value.style.transform = `translate3d(${mouseX}px, ${mouseY}px, 0)`
      }
      rafId = requestAnimationFrame(moveCursor)
    }

    const updateCursor = (e) => {
      mouseX = e.clientX
      mouseY = e.clientY
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
      window.addEventListener('mousemove', updateCursor, { passive: true })
      window.addEventListener('mouseover', handleMouseOver, { passive: true })
      window.addEventListener('mouseout', handleMouseOut, { passive: true })
      rafId = requestAnimationFrame(moveCursor)
    })

    onUnmounted(() => {
      window.removeEventListener('mousemove', updateCursor)
      window.removeEventListener('mouseover', handleMouseOver)
      window.removeEventListener('mouseout', handleMouseOut)
      if (rafId) cancelAnimationFrame(rafId)
    })

    return { cursorRef, isHovering, isVisible }
  }
}
</script>

<template>
  <div 
    ref="cursorRef"
    class="custom-cursor"
    :class="{ 'is-hovering': isHovering, 'is-visible': isVisible }"
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
