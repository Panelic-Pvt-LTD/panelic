<template>
  <div class="preloader" :class="{ 'preloader-hidden': !show }">
    <div class="preloader-content">
      <div class="loader">
        <div class="loader-ring"></div>
        <div class="loader-line"></div>
      </div>
      <div class="preloader-text">
        <h1>PANELIC</h1>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Preloader',
  props: {
    show: {
      type: Boolean,
      default: true
    }
  }
}
</script>

<style scoped>
.preloader {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  background: #050505;
  z-index: 100;
  transition: opacity 0.6s ease, visibility 0.6s ease;
}

.preloader-hidden {
  opacity: 0;
  visibility: hidden;
  pointer-events: none;
}

.preloader-content {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 2rem;
}

/* Minimalistic loader */
.loader {
  position: relative;
  width: 80px;
  height: 80px;
}

.loader-ring {
  position: absolute;
  width: 100%;
  height: 100%;
  border: 2px solid rgba(255, 255, 255, 0.05);
  border-top: 2px solid #7c3aed;
  border-radius: 50%;
  animation: spin 1.5s linear infinite;
}

.loader-line {
  position: absolute;
  top: 50%;
  left: 50%;
  width: 40%;
  height: 2px;
  background: linear-gradient(to right, #7c3aed, rgba(124, 58, 237, 0));
  transform-origin: left;
  animation: rotate 1.5s linear infinite;
}

@keyframes spin {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}

@keyframes rotate {
  0% {
    transform: translateX(-50%) rotate(0deg);
  }
  100% {
    transform: translateX(-50%) rotate(360deg);
  }
}

.preloader-text {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.preloader-text h1 {
  font-size: 28px;
  font-weight: 800;
  letter-spacing: 4px;
  background: linear-gradient(90deg, #fff, #a594ff);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  opacity: 0;
  animation: fadeIn 0.6s ease-out forwards 0.3s;
}

@keyframes fadeIn {
  from {
    opacity: 0;
    transform: translateY(10px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}
</style> 