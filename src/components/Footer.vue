<template>
  <footer class="footer">
    <p>© {{ currentYear }} HAL. All rights reserved.</p>
  </footer>
</template>

<script>
export default {
  name: 'PhanDitFooter',
  data() {
    return {
      currentYear: new Date().getFullYear()
    }
  }
}
</script>

<style scoped>
.footer {
  background-color: #222;
  color: #ccc;
  padding: 15px;
  text-align: center;
  font-size: 14px;
  border-top: 2px solid #444;
  box-shadow: 0 -2px 5px rgba(0, 0, 0, 0.2);
}

.footer p {
  margin: 0;
  font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif;
}
</style>
