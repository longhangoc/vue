<template>
  <header class="youtube-header">
    <div class="header-left">
      <button class="menu-toggle">
        <svg viewBox="0 0 24 24" width="24" height="24">
          <path d="M3 18h18v-2H3v2zm0-5h18v-2H3v2zm0-7v2h18V6H3z"></path>
        </svg>
      </button>
      <div class="logo">
        <h1>LONGHA</h1>
      </div>
    </div>
    <div class="header-right">
      <button class="search-btn">
        <svg viewBox="0 0 24 24" width="24" height="24">
          <path d="M15.5 14h-.79l-.28-.27A6.471 6.471 0 0 0 16 9.5 6.5 6.5 0 1 0 9.5 16c1.61 0 3.09-.59 4.23-1.57l.27.28v.79l5 4.99L20.49 19l-4.99-5zm-6 0C7.01 14 5 11.99 5 9.5S7.01 5 9.5 5 14 7.01 14 9.5 11.99 14 9.5 14z"></path>
        </svg>
      </button>
      <button class="user-btn">
        <svg viewBox="0 0 24 24" width="24" height="24">
          <path d="M12 2C6.48 2 2 6.48 2 12s4.48 10 10 10 10-4.48 10-10S17.52 2 12 2zm0 3c1.66 0 3 1.34 3 3s-1.34 3-3 3-3-1.34-3-3 1.34-3 3-3zm0 14.2c-2.5 0-4.71-1.28-6-3.22.03-1.99 4-3.08 6-3.08 1.99 0 5.97 1.09 6 3.08-1.29 1.94-3.5 3.22-6 3.22z"></path>
        </svg>
      </button>
    </div>
  </header>
</template>

<script>
export default {
  name: 'PhanDauHeader'
}
</script>

<style scoped>
.youtube-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0.5rem 1rem;
  background-color: white;
  border-bottom: 1px solid #e0e0e0;
  height: 56px;
}

.header-left {
  display: flex;
  align-items: center;
  gap: 1rem;
}

.menu-toggle, .search-btn, .user-btn {
  background: none;
  border: none;
  cursor: pointer;
  padding: 8px;
  border-radius: 50%;
  transition: background-color 0.2s;
}

.menu-toggle:hover, 
.search-btn:hover, 
.user-btn:hover {
  background-color: #f0f0f0;
}

.menu-toggle svg, 
.search-btn svg, 
.user-btn svg {
  fill: #030303;
}

.logo h1 {
  font-size: 1.5rem;
  font-weight: 700;
  color: #030303;
  margin: 0;
}

.header-right {
  display: flex;
  align-items: center;
  gap: 1rem;
}

@media (max-width: 600px) {
  .youtube-header {
    padding: 0.5rem;
  }
  
  .logo h1 {
    font-size: 1.2rem;
  }
}
</style>
