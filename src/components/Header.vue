<template>
  <header class="galaxy-header">
    <div class="header-content">
      <h1 class="galaxy-logo">LONGHA</h1>
    </div>
  </header>
</template>

<script>
export default {
  name: 'GalaxyHeader'
}
</script>

<style scoped>
.galaxy-header {
  width: 100%;
  height: 60px;
  background: linear-gradient(135deg, #0c0c1e, #1a1a2e);
  display: flex;
  align-items: center;
  justify-content: center;
  box-shadow: 0 4px 15px rgba(26, 26, 46, 0.5);
}

.galaxy-logo {
  color: transparent;
  background: linear-gradient(45deg, #00bfff, #1e90ff);
  background-clip: text;
  -webkit-background-clip: text;
  font-size: 2rem;
  font-weight: bold;
  letter-spacing: 2px;
  text-transform: uppercase;
}

@media (max-width: 600px) {
  .galaxy-logo {
    font-size: 1.5rem;
  }
}
</style>
