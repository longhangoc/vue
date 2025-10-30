<template>
  <div class="app-container">
    <header class="pro-header">
      <div class="header-left">
        <div class="logo-pro-container" @click="handleLogoClick">
          <div class="logo-pro-circle" :style="{ background: `linear-gradient(135deg, ${logoColors.start}, ${logoColors.end})` }">
            <span class="logo-pro-initial">L</span>
          </div>
          <span class="brand-pro">LONG HA'S</span>
        </div>
      </div>
      <div class="header-center">
        <span class="slogan-pro">Life Wheel App</span>
      </div>
      <div class="header-right">
        <button class="icon-button notification-icon" @click="toggleNotifications">
          <svg xmlns="http://www.w3.org/2000/svg" width="22" height="22" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M18 8A6 6 0 0 0 6 8c0 7-3 9-3 9h18s-3-2-3-9"/><path d="M13.73 21a2 2 0 0 1-3.46 0"/></svg>
          <span class="notification-dot" v-if="hasNotifications"></span>
        </button>
        <div class="avatar-pro" title="User Profile">
          <img :src="avatarUrl" alt="Avatar" />
        </div>
        <button class="icon-button menu-icon" @click="toggleMenu">
          <svg xmlns="http://www.w3.org/2000/svg" width="22" height="22" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><line x1="3" y1="12" x2="21" y2="12"></line><line x1="3" y1="6" x2="21" y2="6"></line><line x1="3" y1="18" x2="21" y2="18"></line></svg>
        </button>
      </div>
    </header>
  </div>
</template>

<script>
export default {
  name: 'ProHeader',
  data() {
    return {
      logoColors: {
        start: '#4F46E5',
        end: '#06B6D4'
      },
      hasNotifications: true,
      avatarUrl: 'https://randomuser.me/api/portraits/men/32.jpg'
    }
  },
  methods: {
    handleLogoClick() {
      this.$router.push('/');
    },
    toggleNotifications() {
      this.hasNotifications = !this.hasNotifications;
    },
    toggleMenu() {
      // Menu logic here
    }
  }
}
</script>

<style scoped>
.pro-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 12px 32px 12px 24px;
  background: #fff;
  border-bottom: 1.5px solid #ececff;
  box-shadow: 0 4px 14px 0 #d6e7ff26;
  border-radius: 0 0 18px 18px;
  min-height: 62px;
  position: sticky;
  top: 0; z-index: 100;
}
.logo-pro-container {
  display: flex;
  align-items: center;
  cursor: pointer;
  gap: 10px;
}
.logo-pro-circle {
  width: 44px; height: 44px;
  border-radius: 50%;
  display: flex; align-items: center; justify-content: center;
  box-shadow: 0 2px 6px #bdbfff19;
}
.logo-pro-initial {
  font-weight: bold;
  color: #fff; font-size: 1.6em;
  letter-spacing: 2px;
}
.brand-pro {
  font-size: 1.55em;
  font-weight: bolder;
  color: #2d326d;
  letter-spacing: 1.1px;
}
.header-center {
  flex: 1;
  display: flex;
  justify-content: center;
}
.slogan-pro {
  font-size: 1.19em;
  color: #5c67b4;
  font-weight: 500;
  letter-spacing: 1px;
  opacity: 0.82;
}
.header-right {
  display: flex;
  align-items: center;
  gap: 18px;
}
.icon-button {
  background: none;
  border: none;
  cursor: pointer;
  padding: 4px 8px;
  border-radius: 12px;
  transition: background 0.18s;
  position: relative;
}
.icon-button:hover {
  background: #edf3ff;
}
.notification-dot {
  position: absolute;
  top: 6px;
  right: 7px;
  width: 8px;
  height: 8px;
  background: #ff6077;
  border-radius: 50%;
  border: 1.5px solid #fff;
}
.avatar-pro {
  width: 39px; height: 39px;
  border-radius: 50%;
  overflow: hidden;
  box-shadow: 0 2px 6px #bdbfff1e;
  margin-left: 1px;
  margin-right: 0;
  border: 2px solid #e9eaff;
}
.avatar-pro img {
  width: 100%; height: 100%; object-fit: cover;
  border-radius: 9999px;
}
@media (max-width: 700px) {
  .header-center { display: none; }
  .brand-pro { font-size: 1.1em; }
  .slogan-pro { font-size: 0.98em; }
  .pro-header { padding: 10px 6vw; }
}
</style>
