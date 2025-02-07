<template>
  <div id="app">
    <PhanDauHeader />
    <div class="content">
      <HelloWorld msg="Welcome to Your Vue.js App" />
      <!-- Hiển thị phần Hướng Dẫn Sử Dụng -->
      <HuongDanSuDung />
    </div>
    <PhanDitFooter />
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import PhanDauHeader from './components/Header.vue'
import PhanDitFooter from './components/Footer.vue'
import HuongDanSuDung from './components/HuongDanSuDung.vue'
export default {
  name: 'App',
  components: {
    PhanDauHeader,
    PhanDitFooter,
    HuongDanSuDung,
    HelloWorld
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  display: flex;
  flex-direction: column;
  height: 100vh;
}
.content {
  flex: 1;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
</style>
