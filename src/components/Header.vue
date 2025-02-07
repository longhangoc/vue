<template>
  <header class="galaxy-header">
    <div class="galaxy-background">
      <div class="stars"></div>
      <div class="shooting-stars">
        <div 
          v-for="star in shootingStars" 
          :key="star.id" 
          class="shooting-star"
          :style="{
            left: `${star.left}%`,
            animationDelay: `${star.delay}s`,
            width: `${star.width}px`
          }"
        ></div>
      </div>
      <div class="nebula"></div>
    </div>
    <div class="header-content">
      <div class="logo-container">
        <h1 class="galaxy-logo">
          <span class="logo-text">LONGHA</span>
          <span class="logo-subtext">❤️</span>
        </h1>
      </div>
    </div>
  </header>
</template>

<script>
export default {
  name: 'GalaxyHeader',
  data() {
    return {
      shootingStars: Array.from({ length: 15 }, (_, index) => ({
        id: index,
        left: Math.random() * 100,
        delay: Math.random() * 5,
        width: 2 + Math.random() * 3
      }))
    }
  }
}
</script>

<style scoped>
.galaxy-header {
  position: relative;
  width: 100%;
  height: 70px;
  background-color: #0c0c1e;
  overflow: hidden;
  display: flex;
  align-items: center;
  justify-content: center;
  box-shadow: 0 4px 15px rgba(0, 0, 255, 0.2);
}

.galaxy-background {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  overflow: hidden;
}

.stars {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-image: 
    radial-gradient(#ffffff 1px, transparent 1px),
    radial-gradient(#ffffff 1px, transparent 1px);
  background-size: 50px 50px;
  background-position: 0 0, 25px 25px;
  animation: twinkle 3s infinite alternate;
}

@keyframes twinkle {
  0% { opacity: 0.6; }
  100% { opacity: 1; }
}

.shooting-stars {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
}

.shooting-star {
  position: absolute;
  top: -10px;
  height: 2px;
  background: linear-gradient(to right, rgba(255,255,255,0.8), transparent);
  transform: rotate(-45deg);
  animation: shootingStar 3s linear infinite;
  z-index: 10;
}

@keyframes shootingStar {
  0% {
    transform: translateX(-100%) rotate(-45deg);
    opacity: 0;
  }
  50% {
    opacity: 1;
  }
  100% {
    transform: translateX(100vw) rotate(-45deg);
    opacity: 0;
  }
}

.nebula {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: radial-gradient(
    ellipse at center, 
    rgba(87, 10, 160, 0.2) 0%, 
    rgba(12, 12, 30, 0) 70%
  );
  animation: nebula-flow 10s ease-in-out infinite alternate;
}

@keyframes nebula-flow {
  0% { transform: scale(1); opacity: 0.5; }
  100% { transform: scale(1.1); opacity: 0.7; }
}

.header-content {
  position: relative;
  z-index: 20;
  display: flex;
  align-items: center;
  justify-content: center;
  width: 100%;
}

.logo-container {
  text-align: center;
}

.galaxy-logo {
  margin: 0;
  display: flex;
  flex-direction: column;
  align-items: center;
  line-height: 1;
}

.logo-text {
  font-size: 2.5rem;
  font-weight: 900;
  background: linear-gradient(
    to right, 
    #00bfff, 
    #1e90ff, 
    #4169e1, 
    #0000cd
  );
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  text-shadow: 0 0 10px rgba(30, 144, 255, 0.5);
  transition: transform 0.3s ease;
}

.logo-subtext {
  font-size: 0.8rem;
  color: #87cefa;
  letter-spacing: 3px;
  text-transform: uppercase;
  margin-top: 5px;
}

.logo-text:hover {
  transform: scale(1.05);
}

@media (max-width: 600px) {
  .galaxy-header {
    height: 60px;
  }

  .logo-text {
    font-size: 2rem;
  }

  .logo-subtext {
    font-size: 0.7rem;
  }
}
</style>
