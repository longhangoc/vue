<template>
  <div class="simple-header">
    <div class="header-logo">
      <div class="logo-circle">
        <span class="logo-initial">L</span>
      </div>
      <span class="header-title">Life Wheel</span>
    </div>
    <div class="header-desc">Tự đánh giá cân bằng các lĩnh vực cuộc sống</div>
  </div>
</template>

<script>
export default {
  name: 'SimpleHeader',
}
</script>

<style scoped>
.simple-header {
  display: flex;
  flex-direction: column;
  align-items: center;
  background: #fff;
  padding: 18px 0 14px 0;
  border-bottom: 1.5px solid #ececff;
  box-shadow: 0 4px 14px 0 #d6e7ff26;
  border-radius: 0 0 14px 14px;
}
.header-logo {
  display: flex;
  align-items: center;
  gap: 12px;
}
.logo-circle {
  width: 40px; height: 40px;
  border-radius: 50%;
  background: linear-gradient(135deg, #4F46E5, #06B6D4);
  display: flex; align-items: center; justify-content: center;
}
.logo-initial {
  font-size: 1.3em; color: #fff; font-weight: bold; letter-spacing: 1px;
}
.header-title {
  font-size: 1.45em;
  font-weight: 700;
  color: #2d326d;
  letter-spacing: 1px;
}
.header-desc {
  margin-top: 7px;
  font-size: 1em;
  color: #5c67b4;
  opacity: 0.88;
  text-align: center;
}
</style>
