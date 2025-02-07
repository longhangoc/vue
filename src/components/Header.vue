<template>
  <div class="app-container">
    <header class="app-header">
      <div class="header-left">
        <div class="logo-container">
          <div class="logo-circle" :style="{ background: `linear-gradient(135deg, ${logoColors.start}, ${logoColors.end})` }"></div>
          <span class="logo-text">LONG HA'S projects</span>
        </div>
        <div class="dropdown-icon">
          <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
            <path d="m6 9 6 6 6-6"/>
          </svg>
        </div>
      </div>
      <div class="header-right">
        <div class="header-icons">
          <div class="notification-icon">
            <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
              <path d="M18 8A6 6 0 0 0 6 8c0 7-3 9-3 9h18s-3-2-3-9"/>
              <path d="M13.73 21a2 2 0 0 1-3.46 0"/>
            </svg>
            <span class="notification-dot"></span>
          </div>
          <div class="menu-icon">
            <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
              <line x1="3" y1="12" x2="21" y2="12"></line>
              <line x1="3" y1="6" x2="21" y2="6"></line>
              <line x1="3" y1="18" x2="21" y2="18"></line>
            </svg>
          </div>
        </div>
      </div>
    </header>


    <router-view class="page-content"></router-view>
  </div>
</template>

<script>
export default {
  name: 'ProjectApp',
  data() {
    return {
      logoColors: {
        start: '#ff6b6b',
        end: '#4ecdc4'
      }
    }
  }
}
</script>

<style scoped>
.app-container {
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
}

.app-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 12px 16px;
  border-bottom: 1px solid #e1e4e8;
}

.header-left {
  display: flex;
  align-items: center;
  gap: 12px;
}

.logo-container {
  display: flex;
  align-items: center;
  gap: 10px;
}

.logo-circle {
  width: 32px;
  height: 32px;
  border-radius: 50%;
}

.logo-text {
  font-weight: 600;
  color: #24292e;
}

.dropdown-icon svg {
  color: #586069;
}

.header-right {
  display: flex;
  align-items: center;
}

.header-icons {
  display: flex;
  align-items: center;
  gap: 16px;
}

.notification-icon {
  position: relative;
}

.notification-dot {
  position: absolute;
  top: -4px;
  right: -4px;
  width: 10px;
  height: 10px;
  background-color: #ff4d4f;
  border-radius: 50%;
}

.app-nav {
  display: flex;
  border-bottom: 1px solid #e1e4e8;
}

.nav-item {
  padding: 12px 16px;
  text-decoration: none;
  color: #24292e;
  font-weight: 500;
}

.nav-item.active {
  border-bottom: 2px solid #0366d6;
  color: #0366d6;
}

.page-content {
  padding: 20px;
}
</style>
