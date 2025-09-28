<template>
  <div class="code-background">
    <div class="geometric-bg">
      <div class="grid-pattern"></div>
      <div class="floating-elements">
        <div v-for="i in 12" :key="i" class="floating-icon" :style="getFloatingStyle(i)">
          {{ getTechIcon(i) }}
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
const techIcons = ['⚡', '🚀', '💻', '💿', '🖨️', '📱', '🌐', '🖥️', '📊', '⌨️', '🔥', '💾', '🖱️', '📟', '⚙️', '🔌']

const getTechIcon = (index) => {
  return techIcons[(index - 1) % techIcons.length]
}

const getFloatingStyle = (index) => {
  const positions = [
    { top: '10%', left: '15%', animationDelay: '0s' },
    { top: '20%', left: '85%', animationDelay: '1s' },
    { top: '35%', left: '25%', animationDelay: '2s' },
    { top: '45%', left: '75%', animationDelay: '0.5s' },
    { top: '60%', left: '10%', animationDelay: '1.5s' },
    { top: '70%', left: '90%', animationDelay: '2.5s' },
    { top: '15%', left: '50%', animationDelay: '3s' },
    { top: '40%', left: '60%', animationDelay: '0.8s' },
    { top: '75%', left: '40%', animationDelay: '1.8s' },
    { top: '25%', left: '70%', animationDelay: '2.2s' },
    { top: '55%', left: '20%', animationDelay: '1.2s' },
    { top: '80%', left: '65%', animationDelay: '2.8s' }
  ]
  
  return positions[(index - 1) % positions.length]
}
</script>

<style scoped>
.code-background {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: 1;
  overflow: hidden;
}

.geometric-bg {
  width: 100%;
  height: 100%;
  background: linear-gradient(135deg, #3b82f6 0%, #1e40af 100%);
  position: relative;
}

.grid-pattern {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-image: 
    linear-gradient(rgba(255,255,255,0.15) 1px, transparent 1px),
    linear-gradient(90deg, rgba(255,255,255,0.15) 1px, transparent 1px);
  background-size: 50px 50px;
  animation: gridMove 15s linear infinite;
}

.floating-elements {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
}

.floating-icon {
  position: absolute;
  font-size: 2rem;
  opacity: 0.8;
  animation: float 4s ease-in-out infinite;
  user-select: none;
  pointer-events: none;
}

@keyframes gridMove {
  0% { transform: translate(0, 0); }
  100% { transform: translate(50px, 50px); }
}

@keyframes float {
  0%, 100% {
    transform: translateY(0px) rotate(0deg);
    opacity: 0.8;
  }
  50% {
    transform: translateY(-30px) rotate(10deg);
    opacity: 1;
  }
}

@media (max-width: 768px) {
  .floating-icon {
    font-size: 1.5rem;
  }
  
  .grid-pattern {
    background-size: 30px 30px;
  }
}

@media (max-width: 480px) {
  .floating-icon {
    font-size: 1rem;
  }
  
  .grid-pattern {
    background-size: 20px 20px;
  }
}
</style>