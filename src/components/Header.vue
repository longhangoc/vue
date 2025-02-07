<template>
  <header class="header">
    <h1>LONGHA</h1>
  </header>
</template>

<script>
export default {
  name: 'PhanDauHeader'
}
</script>

<style scoped>
.header {
  display: flex;
  justify-content: center;
  align-items: center;
  /* Animated gradient background */
  background: linear-gradient(90deg, #6a11cb, #2575fc);
  background-size: 200% 200%;
  animation: gradientAnimation 5s ease infinite;
  padding: 30px 20px;
  color: #fff;
  font-size: 2.5rem;
  font-weight: 700;
  text-shadow: 0 2px 4px rgba(0, 0, 0, 0.3);
  border-bottom: 2px solid rgba(255, 255, 255, 0.2);
}

/* Animation keyframes cho background */
@keyframes gradientAnimation {
  0% {
    background-position: 0% 50%;
  }
  50% {
    background-position: 100% 50%;
  }
  100% {
    background-position: 0% 50%;
  }
}
</style>
