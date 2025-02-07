<template>
  <header class="header">
    <div class="logo">My Website</div>
    <nav class="nav">
      <a href="#">Trang chủ</a>
      <a href="#">Dịch vụ</a>
      <a href="#">Về chúng tôi</a>
      <a href="#">Liên hệ</a>
    </nav>
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
  justify-content: space-between;
  align-items: center;
  background-color: #2c3e50;
  padding: 15px 30px;
  color: white;
}
.logo {
  font-size: 24px;
  font-weight: bold;
}
.nav a {
  color: white;
  text-decoration: none;
  margin-left: 20px;
  font-size: 18px;
  transition: color 0.3s;
}
.nav a:hover {
  color: #42b983;
}
</style>
