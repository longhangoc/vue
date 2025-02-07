<template>
  <header class="header">
    <div class="header-content">
      <div class="header-gradient"></div>
      <div class="header-title-wrapper">
        <h1 class="header-title">
          <span class="logo-icon">
            <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
              <path d="M12 22s8-4 8-10V5l-8-3-8 3v7c0 6 8 10 8 10z"></path>
            </svg>
          </span>
          LONGHA
        </h1>
      </div>
    </div>
  </header>
</template>

<script>
export default {
  name: 'PhanDauHeader'
}
</script>

<style scoped>
.header {
  position: relative;
  background: linear-gradient(135deg, #6a11cb 0%, #2575fc 100%);
  color: white;
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 4rem 2rem;
  overflow: hidden;
  box-shadow: 0 4px 15px rgba(0,0,0,0.2);
}

.header-content {
  position: relative;
  z-index: 10;
  text-align: center;
}

.header-gradient {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: linear-gradient(135deg, #6a11cb 0%, #2575fc 100%);
  animation: gradient-flow 5s ease infinite;
  opacity: 0.7;
}

.header-title-wrapper {
  position: relative;
  z-index: 20;
}

.header-title {
  font-size: 4rem;
  font-weight: 800;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 1rem;
  text-transform: uppercase;
  letter-spacing: 0.05em;
  text-shadow: 0 4px 10px rgba(0,0,0,0.3);
}

.logo-icon {
  width: 3rem;
  height: 3rem;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  stroke: currentColor;
  color: #ffd700;
  transform: translateY(-0.2rem);
}

.logo-icon svg {
  width: 100%;
  height: 100%;
}

@keyframes gradient-flow {
  0% { background-position: 0% 50%; }
  50% { background-position: 100% 50%; }
  100% { background-position: 0% 50%; }
}

@media (max-width: 768px) {
  .header-title {
    font-size: 2.5rem;
    gap: 0.5rem;
  }

  .logo-icon {
    width: 2rem;
    height: 2rem;
  }
}
</style>
