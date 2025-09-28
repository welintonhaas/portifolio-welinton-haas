<template>
  <div class="portfolio-container">
    <NuxtRouteAnnouncer />
    <CodeBackground />
    <Portfolio />
  </div>
</template>

<style>
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap');

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
  background-color: #f8fafc;
  color: #2d3748;
  overflow-x: hidden;
  line-height: 1.6;
}

.portfolio-container {
  position: relative;
  min-height: 100vh;
}

html {
  scroll-behavior: smooth;
}
</style>