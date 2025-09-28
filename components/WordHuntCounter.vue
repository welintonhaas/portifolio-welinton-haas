<template>
  <div class="word-hunt-counter" v-if="showCounter">
    <div class="counter-content">
      <div class="counter-header">
        <span class="hunt-icon">🔍</span>
        <span class="counter-title">Caça-Palavras</span>
      </div>
      <div class="counter-stats">
        <span class="found-count">{{ foundWords.size }}</span>
        <span class="separator">/</span>
        <span class="total-count">{{ totalWords }}</span>
      </div>
      <div class="progress-bar">
        <div 
          class="progress-fill" 
          :style="{ width: `${(foundWords.size / totalWords) * 100}%` }"
        ></div>
      </div>
      <div class="hint-text">
        Encontre links e palavras escondidas no código!
      </div>
    </div>
  </div>
</template>

<script setup>
const foundWords = ref(new Set())
const totalWords = 22 // 9 links + 13 palavras escondidas
const showCounter = ref(true)

// Escutar eventos de palavras encontradas
onMounted(() => {
  const handleWordFound = (event) => {
    if (event.detail && event.detail.word) {
      foundWords.value.add(event.detail.word)
      
      if (foundWords.value.size === totalWords) {
        setTimeout(() => {
          showCounter.value = false
        }, 3000)
      }
    }
  }
  
  // Escutar clicks nas palavras escondidas
  const handleClick = (event) => {
    if (event.target.classList.contains('hidden-word')) {
      const word = event.target.dataset.word
      if (word && !foundWords.value.has(word)) {
        foundWords.value.add(word)
      }
    }
  }
  
  document.addEventListener('click', handleClick)
  window.addEventListener('wordFound', handleWordFound)
  
  onUnmounted(() => {
    document.removeEventListener('click', handleClick)
    window.removeEventListener('wordFound', handleWordFound)
  })
})
</script>

<style scoped>
.word-hunt-counter {
  position: fixed;
  top: 20px;
  right: 20px;
  z-index: 1000;
  background: rgba(13, 17, 23, 0.9);
  border: 1px solid #30363d;
  border-radius: 12px;
  padding: 15px;
  backdrop-filter: blur(10px);
  min-width: 200px;
  box-shadow: 0 8px 32px rgba(0, 0, 0, 0.3);
}

.counter-content {
  text-align: center;
}

.counter-header {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 8px;
  margin-bottom: 10px;
}

.hunt-icon {
  font-size: 1.2em;
}

.counter-title {
  color: #79c0ff;
  font-family: 'Fira Code', monospace;
  font-weight: 600;
  font-size: 0.9em;
}

.counter-stats {
  margin-bottom: 10px;
}

.found-count {
  color: #58a6ff;
  font-size: 1.5em;
  font-weight: 700;
  font-family: 'Fira Code', monospace;
}

.separator {
  color: #8b949e;
  margin: 0 5px;
  font-size: 1.2em;
}

.total-count {
  color: #8b949e;
  font-size: 1.2em;
  font-family: 'Fira Code', monospace;
}

.progress-bar {
  width: 100%;
  height: 6px;
  background: rgba(48, 54, 61, 0.5);
  border-radius: 3px;
  overflow: hidden;
  margin-bottom: 10px;
}

.progress-fill {
  height: 100%;
  background: linear-gradient(90deg, #58a6ff, #79c0ff);
  border-radius: 3px;
  transition: width 0.5s ease;
  position: relative;
}

.progress-fill::after {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.2), transparent);
  animation: shimmer 2s infinite;
}

@keyframes shimmer {
  0% { transform: translateX(-100%); }
  100% { transform: translateX(100%); }
}

.hint-text {
  color: #8b949e;
  font-size: 0.8em;
  font-family: 'Fira Code', monospace;
  line-height: 1.2;
}

@media (max-width: 768px) {
  .word-hunt-counter {
    top: 10px;
    right: 10px;
    padding: 12px;
    min-width: 150px;
  }
  
  .counter-title {
    font-size: 0.8em;
  }
  
  .found-count {
    font-size: 1.3em;
  }
  
  .hint-text {
    font-size: 0.7em;
  }
}

@media (max-width: 480px) {
  .word-hunt-counter {
    top: 5px;
    right: 5px;
    padding: 10px;
    min-width: 120px;
  }
  
  .counter-header {
    flex-direction: column;
    gap: 4px;
  }
  
  .counter-title {
    font-size: 0.7em;
  }
  
  .found-count {
    font-size: 1.1em;
  }
  
  .hint-text {
    font-size: 0.6em;
  }
}
</style>