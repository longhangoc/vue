<template>
  <header class="love-header">
    <div class="heart-background">
      <div class="falling-hearts">
        <div v-for="heart in hearts" :key="heart.id" 
             class="heart" 
             :style="{
               left: `${heart.left}%`, 
               animationDelay: `${heart.delay}s`,
               transform: `scale(${heart.scale})`
             }">
          ❤️
        </div>
      </div>
    </div>
    <div class="header-content">
      <div class="logo-container">
        <h1 class="logo">LONGHA</h1>
      </div>
    </div>
  </header>
</template>

<script>
export default {
  name: 'LoveHeader',
  data() {
    return {
      hearts: Array.from({ length: 10 }, (_, index) => ({
        id: index,
        left: Math.random() * 100,
        delay: Math.random() * 10,
        scale: 0.5 + Math.random() * 0.5
      }))
    }
  }
}
</script>

<style scoped>
.love-header {
  position: relative;
  width: 100%;
  height: 60px;
  background: linear-gradient(135deg, #fff0f5, #ffebee);
  overflow: hidden;
  display: flex;
  align-items: center;
  justify-content: center;
  box-shadow: 0 2px 10px rgba(0,0,0,0.05);
}

.heart-background {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  pointer-events: none;
  overflow: hidden;
}

.falling-hearts {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
}

.heart {
  position: absolute;
  font-size: 20px;
  opacity: 0.6;
  animation: fall 10s linear infinite;
  user-select: none;
}

@keyframes fall {
  0% {
    transform: translateY(-20px);
    opacity: 0.6;
  }
  100% {
    transform: translateY(calc(100vh + 20px));
    opacity: 0;
  }
}

.logo-container {
  z-index: 10;
  position: relative;
}

.logo {
  margin: 0;
  font-size: 2rem;
  font-weight: 800;
  background: linear-gradient(45deg, #ff6b6b, #ff4757);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  text-align: center;
  transition: transform 0.3s ease;
}

.logo:hover {
  transform: scale(1.05);
}

@media (max-width: 600px) {
  .logo {
    font-size: 1.5rem;
  }

  .heart {
    font-size: 15px;
  }
}
</style>
