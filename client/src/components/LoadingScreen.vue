<template>
  <div class="loading-overlay">
    <div class="loader-content">
      <div class="spinner">
        <div class="gradient-ring"></div>
        <div class="inner-circle"></div>
      </div>
      <p class="loading-text">Loading Experience...</p>
    </div>
  </div>
</template>

<style scoped>
.loading-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  background: radial-gradient(circle at center, #1a1a2e 0%, #0b0b12 100%);
  z-index: 9999;
}

.loader-content {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 2rem;
}

.spinner {
  position: relative;
  width: 80px;
  height: 80px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.gradient-ring {
  position: absolute;
  width: 100%;
  height: 100%;
  border-radius: 50%;
  background: conic-gradient(from 0deg, #00f2fe 0%, #4facfe 25%, #f093fb 50%, #f5576c 75%, #00f2fe 100%);
  animation: spin 1.5s linear infinite;
}

.gradient-ring::after {
  content: '';
  position: absolute;
  top: -4px;
  left: -4px;
  right: -4px;
  bottom: -4px;
  background: inherit;
  border-radius: 50%;
  filter: blur(12px);
  opacity: 0.8;
  z-index: -1;
}

.inner-circle {
  width: 76%;
  height: 76%;
  background: #0d0d16;
  border-radius: 50%;
  z-index: 1;
}

.loading-text {
  color: #fff;
  font-family: 'Inter', system-ui, -apple-system, sans-serif;
  font-size: 1.15rem;
  font-weight: 500;
  letter-spacing: 0.1em;
  text-transform: uppercase;
  animation: pulse 2s ease-in-out infinite;
}

@keyframes spin {
  0% { transform: rotate(0deg); }
  100% { transform: rotate(360deg); }
}

@keyframes pulse {
  0%, 100% { opacity: 0.5; text-shadow: none; }
  50% { opacity: 1; text-shadow: 0 0 15px rgba(255, 255, 255, 0.4); }
}
</style>
