<template>
  <div class="app-container">
    <header class="app-header">
      <div class="header-left">
        <div class="logo-container" @click="handleLogoClick">
          <div
            class="logo-circle"
            :style="{ background: `linear-gradient(135deg, ${logoColors.start}, ${logoColors.end})` }"
          >
            <span class="logo-initial">L</span>
          </div>
          <div class="logo-text-container">
            <span class="logo-text">LONG HA'S</span>
            <span class="logo-subtext">projects</span>
          </div>
          <div
            class="dropdown-icon"
            :class="{ 'is-active': isDropdownOpen }"
            @click.stop="toggleDropdown"
          >
            <svg
              xmlns="http://www.w3.org/2000/svg"
              width="20"
              height="20"
              viewBox="0 0 24 24"
              fill="none"
              stroke="currentColor"
              stroke-width="2"
              stroke-linecap="round"
              stroke-linejoin="round"
            >
              <path d="m6 9 6 6 6-6" />
            </svg>
          </div>
        </div>
      </div>

      <div class="header-right">
        <div class="search-bar">
          <svg
            xmlns="http://www.w3.org/2000/svg"
            width="18"
            height="18"
            viewBox="0 0 24 24"
            fill="none"
            stroke="currentColor"
            stroke-width="2"
            stroke-linecap="round"
            stroke-linejoin="round"
          >
            <circle cx="11" cy="11" r="8"></circle>
            <line x1="21" y1="21" x2="16.65" y2="16.65"></line>
          </svg>
          <input
            type="text"
            placeholder="Search projects..."
            class="search-input"
          />
        </div>

        <div class="header-icons">
          <button class="icon-button notification-icon" @click="toggleNotifications">
            <svg
              xmlns="http://www.w3.org/2000/svg"
              width="20"
              height="20"
              viewBox="0 0 24 24"
              fill="none"
              stroke="currentColor"
              stroke-width="2"
              stroke-linecap="round"
              stroke-linejoin="round"
            >
              <path d="M18 8A6 6 0 0 0 6 8c0 7-3 9-3 9h18s-3-2-3-9"/>
              <path d="M13.73 21a2 2 0 0 1-3.46 0"/>
            </svg>
            <span class="notification-dot" v-if="hasNotifications"></span>
            <span class="tooltip">Notifications</span>
          </button>

          <button class="icon-button menu-icon" @click="toggleMenu">
            <svg
              xmlns="http://www.w3.org/2000/svg"
              width="20"
              height="20"
              viewBox="0 0 24 24"
              fill="none"
              stroke="currentColor"
              stroke-width="2"
              stroke-linecap="round"
              stroke-linejoin="round"
            >
              <line x1="3" y1="12" x2="21" y2="12"></line>
              <line x1="3" y1="6" x2="21" y2="6"></line>
              <line x1="3" y1="18" x2="21" y2="18"></line>
            </svg>
            <span class="tooltip">Menu</span>
          </button>
        </div>
      </div>
    </header>

    <div v-if="isDropdownOpen" class="dropdown-menu" @click="handleDropdownClick">
      <div class="dropdown-item">My Projects</div>
      <div class="dropdown-item">Shared Projects</div>
      <div class="dropdown-item">Archive</div>
    </div>

    <router-view class="page-content"></router-view>
  </div>
</template>

<script>
export default {
  name: 'PhanDauHeader',
  data() {
    return {
      logoColors: {
        start: '#4F46E5',
        end: '#06B6D4'
      },
      isDropdownOpen: false,
      hasNotifications: true,
      searchQuery: ''
    }
  },
  methods: {
    handleLogoClick() {
      this.$router.push('/');
    },
    toggleDropdown() {
      this.isDropdownOpen = !this.isDropdownOpen;
    },
    toggleNotifications() {
      this.hasNotifications = !this.hasNotifications;
    },
    toggleMenu() {
      // Implement menu toggle logic
    },
    handleDropdownClick(event) {
      // Prevent closing when clicking inside dropdown
      event.stopPropagation();
    }
  },
  mounted() {
    // Lưu callback của sự kiện click để xóa sau này
    this._documentClickListener = () => {
      if (this.isDropdownOpen) this.isDropdownOpen = false;
    };
    document.addEventListener('click', this._documentClickListener);
  },
  beforeUnmount() {
    // Xóa đúng event listener đã lưu lại
    document.removeEventListener('click', this._documentClickListener);
  }
}
</script>

<style scoped>
/* (Giữ nguyên phần CSS như cũ) */
.app-container {
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
  position: relative;
}

.app-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 12px 24px;
  background: white;
  border-bottom: 1px solid rgba(0, 0, 0, 0.06);
  box-shadow: 0 1px 3px rgba(0, 0, 0, 0.02);
  position: sticky;
  top: 0;
  z-index: 100;
  backdrop-filter: blur(8px);
}

.header-left {
  display: flex;
  align-items: center;
  gap: 16px;
}

.logo-container {
  display: flex;
  align-items: center;
  gap: 12px;
  cursor: pointer;
  padding: 6px;
  border-radius: 8px;
  transition: all 0.2s ease;
}

.logo-container:hover {
  background: rgba(0, 0, 0, 0.02);
}

.logo-circle {
  width: 36px;
  height: 36px;
  border-radius: 10px;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: transform 0.3s ease;
}

.logo-initial {
  color: white;
  font-weight: 600;
  font-size: 18px;
}

.logo-container:hover .logo-circle {
  transform: scale(1.05);
}

.logo-text-container {
  display: flex;
  flex-direction: column;
  gap: 2px;
}

.logo-text {
  font-weight: 600;
  font-size: 15px;
  color: #111827;
  letter-spacing: -0.01em;
}

.logo-subtext {
  font-size: 13px;
  color: #6B7280;
}

.dropdown-icon {
  padding: 6px;
  border-radius: 6px;
  color: #6B7280;
  transition: all 0.2s ease;
}

.dropdown-icon:hover {
  background: rgba(0, 0, 0, 0.04);
  color: #111827;
}

.dropdown-icon.is-active {
  transform: rotate(180deg);
}

.header-right {
  display: flex;
  align-items: center;
  gap: 20px;
}

.search-bar {
  display: flex;
  align-items: center;
  gap: 8px;
  background: #F9FAFB;
  padding: 8px 12px;
  border-radius: 8px;
  border: 1px solid rgba(0, 0, 0, 0.06);
  transition: all 0.2s ease;
}

.search-bar:focus-within {
  background: white;
  border-color: #4F46E5;
  box-shadow: 0 0 0 3px rgba(79, 70, 229, 0.1);
}

.search-input {
  border: none;
  background: transparent;
  outline: none;
  width: 200px;
  font-size: 14px;
  color: #111827;
}

.search-input::placeholder {
  color: #9CA3AF;
}

.header-icons {
  display: flex;
  align-items: center;
  gap: 8px;
}

.icon-button {
  position: relative;
  padding: 8px;
  border-radius: 8px;
  border: none;
  background: transparent;
  color: #6B7280;
  cursor: pointer;
  transition: all 0.2s ease;
}

.icon-button:hover {
  background: rgba(0, 0, 0, 0.04);
  color: #111827;
}

.notification-dot {
  position: absolute;
  top: 6px;
  right: 6px;
  width: 8px;
  height: 8px;
  background: #EF4444;
  border-radius: 50%;
  border: 2px solid white;
}

.tooltip {
  position: absolute;
  bottom: -30px;
  left: 50%;
  transform: translateX(-50%);
  background: #1F2937;
  color: white;
  padding: 4px 8px;
  border-radius: 4px;
  font-size: 12px;
  white-space: nowrap;
  opacity: 0;
  visibility: hidden;
  transition: all 0.2s ease;
}

.icon-button:hover .tooltip {
  opacity: 1;
  visibility: visible;
}

.dropdown-menu {
  position: absolute;
  top: 100%;
  left: 24px;
  background: white;
  border-radius: 12px;
  box-shadow: 0 10px 25px -5px rgba(0, 0, 0, 0.1);
  border: 1px solid rgba(0, 0, 0, 0.06);
  padding: 6px;
  min-width: 200px;
  z-index: 99;
  animation: slideDown 0.2s ease;
}

.dropdown-item {
  padding: 10px 14px;
  border-radius: 8px;
  color: #374151;
  font-size: 14px;
  cursor: pointer;
  transition: all 0.2s ease;
}

.dropdown-item:hover {
  background: #F9FAFB;
  color: #111827;
}

@keyframes slideDown {
  from {
    opacity: 0;
    transform: translateY(-10px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

/* Responsive Design */
@media (max-width: 768px) {
  .app-header {
    padding: 12px 16px;
  }

  .logo-text-container {
    display: none;
  }

  .search-bar {
    display: none;
  }
}

/* High-DPI Screen Optimizations */
@media (-webkit-min-device-pixel-ratio: 2), (min-resolution: 192dpi) {
  .app-header {
    border-bottom: 0.5px solid rgba(0, 0, 0, 0.06);
  }
}
</style>
