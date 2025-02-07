<template>
  <header class="enhanced-header">
    <div class="header-content">
      <div class="header-left">
        <button 
          class="menu-toggle" 
          @mouseenter="hoverMenu = true" 
          @mouseleave="hoverMenu = false"
          @click="toggleMenu"
        >
          <svg viewBox="0 0 24 24" width="24" height="24">
            <path d="M3 18h18v-2H3v2zm0-5h18v-2H3v2zm0-7v2h18V6H3z"></path>
          </svg>
          <span 
            class="menu-hover-effect" 
            :class="{ 'active': hoverMenu }"
          ></span>
        </button>
        <div class="logo-container">
          <h1 class="logo">
            <span class="logo-text">LONGHA</span>
          </h1>
        </div>
      </div>
    </div>
  </header>
</template>

<script>
export default {
  name: 'EnhancedHeader',
  data() {
    return {
      hoverMenu: false,
      isMenuOpen: false
    }
  },
  methods: {
    toggleMenu() {
      this.isMenuOpen = !this.isMenuOpen
      // You can add additional logic here for menu opening/closing
    }
  }
}
</script>

<style scoped>
.enhanced-header {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  background-color: rgba(255, 255, 255, 0.95);
  backdrop-filter: blur(10px);
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.05);
  z-index: 1000;
  transition: all 0.3s ease;
}

.header-content {
  max-width: 1200px;
  margin: 0 auto;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0.75rem 1rem;
}

.header-left {
  display: flex;
  align-items: center;
  gap: 1.5rem;
}

.menu-toggle {
  position: relative;
  background: none;
  border: none;
  cursor: pointer;
  padding: 10px;
  border-radius: 50%;
  transition: all 0.3s ease;
  overflow: hidden;
}

.menu-toggle svg {
  position: relative;
  z-index: 2;
  fill: #1a1a1a;
  transition: transform 0.3s ease;
}

.menu-toggle:hover svg {
  transform: rotate(90deg);
}

.menu-hover-effect {
  position: absolute;
  top: 50%;
  left: 50%;
  width: 0;
  height: 0;
  background-color: rgba(0, 0, 0, 0.1);
  border-radius: 50%;
  transform: translate(-50%, -50%);
  opacity: 0;
  transition: all 0.3s ease;
}

.menu-toggle:hover .menu-hover-effect.active {
  width: 150%;
  height: 150%;
  opacity: 1;
}

.logo-container {
  display: flex;
  align-items: center;
}

.logo {
  margin: 0;
  font-size: 1.5rem;
  font-weight: 800;
  background: linear-gradient(45deg, #3494E6, #EC6EAD);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  transition: all 0.3s ease;
}

.logo:hover {
  transform: scale(1.05);
}

@media (max-width: 600px) {
  .header-content {
    padding: 0.5rem 0.75rem;
  }

  .logo {
    font-size: 1.2rem;
  }

  .menu-toggle {
    padding: 8px;
  }
}

@media (max-width: 400px) {
  .header-left {
    gap: 1rem;
  }
}
</style>
