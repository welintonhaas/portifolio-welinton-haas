<template>
  <div 
    ref="cursor" 
    class="custom-cursor"
    :class="{ 'cursor-hover': isHovering }"
  >
    <div class="cursor-inner"></div>
  </div>
</template>

<script setup>
const cursor = ref(null)
const isHovering = ref(false)

onMounted(() => {
  let animationId = null
  
  const updateCursor = (e) => {
    if (cursor.value && !animationId) {
      animationId = requestAnimationFrame(() => {
        if (cursor.value) {
          cursor.value.style.transform = `translate(${e.clientX}px, ${e.clientY}px)`
        }
        animationId = null
      })
    }
  }

  const handleMouseEnter = () => {
    isHovering.value = true
  }

  const handleMouseLeave = () => {
    isHovering.value = false
  }

  document.addEventListener('mousemove', updateCursor, { passive: true })
  
  // Detectar elementos interativos dinamicamente
  const detectInteractiveElements = () => {
    const elements = document.querySelectorAll('button, a, .code-section, .contact-link, .form-input, .form-textarea, .hidden-word')
    elements.forEach(el => {
      el.addEventListener('mouseenter', handleMouseEnter, { passive: true })
      el.addEventListener('mouseleave', handleMouseLeave, { passive: true })
    })
    return elements
  }
  
  const interactiveElements = detectInteractiveElements()

  onUnmounted(() => {
    document.removeEventListener('mousemove', updateCursor)
    interactiveElements.forEach(el => {
      el.removeEventListener('mouseenter', handleMouseEnter)
      el.removeEventListener('mouseleave', handleMouseLeave)
    })
    if (animationId) {
      cancelAnimationFrame(animationId)
    }
  })
})
</script>

<style scoped>
.custom-cursor {
  position: fixed;
  top: 0;
  left: 0;
  width: 20px;
  height: 20px;
  border: 2px solid #58a6ff;
  border-radius: 50%;
  pointer-events: none;
  z-index: 9999;
  transform: translate(-10px, -10px);
  transition: width 0.2s ease, height 0.2s ease, border-color 0.2s ease;
  mix-blend-mode: difference;
  will-change: transform;
}

.cursor-inner {
  width: 4px;
  height: 4px;
  background: #58a6ff;
  border-radius: 50%;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}

.cursor-hover {
  width: 40px;
  height: 40px;
  border-color: #ff7b72;
}

.cursor-hover .cursor-inner {
  background: #ff7b72;
  width: 8px;
  height: 8px;
}

@media (max-width: 768px) {
  .custom-cursor {
    display: none;
  }
}
</style>