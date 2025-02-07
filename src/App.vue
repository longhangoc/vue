<template>
  <div id="app">
    <phandau />
    <div class="content">
      <HelloWorld msg="Welcome to Your Vue.js App" />
    </div>
    <phandit />
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import phandau from './components/phandau.vue'
import phandit from './components/phandit.vue'

export default {
  name: 'App',
  components: {
    phandau,
    phandit,
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
  height: 100vh; /* Chiều cao full màn hình */
}

.content {
  flex: 1; /* Chiếm hết phần còn lại giữa header và footer */
  display: flex;
  justify-content: center; /* Căn giữa theo chiều ngang */
  align-items: center; /* Căn giữa theo chiều dọc */
}
</style>
