<template>
  <footer class="footer">
    <p>© 2025 HAL. All rights reserved.</p>
    <div class="social-icons">
      <a href="#"><i class="fab fa-facebook"></i></a>
      <a href="#"><i class="fab fa-twitter"></i></a>
      <a href="#"><i class="fab fa-instagram"></i></a>
    </div>
  </footer>
</template>

<script>
export default {
  name: 'phandit'
}
</script>

<style scoped>
.footer {
  background-color: #34495e;
  color: white;
  text-align: center;
  padding: 20px;
  position: relative;
  bottom: 0;
  width: 100%;
}

.social-icons a {
  color: white;
  font-size: 20px;
  margin: 0 10px;
  transition: color 0.3s;
}

.social-icons a:hover {
  color: #42b983;
}
</style>
