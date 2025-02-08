<!-- Footer.vue -->
<template>
  <footer class="footer">
    <!-- Logo -->
    <div class="logo">▲</div>
    
    <!-- Main Navigation Grid -->
    <div class="nav-grid">
      <div class="nav-item">
        <a href="/" class="nav-link">Home</a>
      </div>
      <div class="nav-item">
        <a href="/docs" class="nav-link">Docs</a>
      </div>
      <div class="nav-item">
        <a href="/guides" class="nav-link">Guides</a>
      </div>
      <div class="nav-item">
        <a href="/help" class="nav-link">Help</a>
      </div>
      <div class="nav-item">
        <a href="/contact" class="nav-link">Contact</a>
      </div>
      <div class="nav-item">
        <div class="dropdown">
          <button class="dropdown-button">
            Legal
            <span class="dropdown-arrow">›</span>
          </button>
        </div>
      </div>
    </div>
    
    <!-- Status Bar -->
    <div class="status-bar">
      <div class="status">
        <span class="status-dot"></span>
        <span class="status-text">All systems normal</span>
      </div>
      
      <div class="tools">
        <button class="tool-button" title="Copy">
          <svg viewBox="0 0 24 24" width="18" height="18" stroke="currentColor" stroke-width="2" fill="none">
            <path d="M8 3H5a2 2 0 0 0-2 2v3m18 0V5a2 2 0 0 0-2-2h-3m0 18h3a2 2 0 0 0 2-2v-3M3 16v3a2 2 0 0 0 2 2h3"/>
          </svg>
        </button>
        <button class="tool-button" title="Theme">
          <svg viewBox="0 0 24 24" width="18" height="18" stroke="currentColor" stroke-width="2" fill="none">
            <circle cx="12" cy="12" r="5"/>
            <path d="M12 1v2m0 18v2M4.22 4.22l1.42 1.42m12.72 12.72l1.42 1.42M1 12h2m18 0h2M4.22 19.78l1.42-1.42M18.36 5.64l1.42-1.42"/>
          </svg>
        </button>
        <button class="tool-button" title="Time">
          <svg viewBox="0 0 24 24" width="18" height="18" stroke="currentColor" stroke-width="2" fill="none">
            <circle cx="12" cy="12" r="10"/>
            <path d="M12 6v6l4 2"/>
          </svg>
        </button>
      </div>
    </div>
    
    <!-- Copyright -->
    <div class="copyright">
      © {{ currentYear }}, Vercel Inc.
    </div>
  </footer>
</template>

<script>
export default {
  name: 'PhanDitFooter',
  computed: {
    currentYear() {
      return new Date().getFullYear()
    }
  }
}
</script>

<style scoped>
.footer {
  padding: 2rem;
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Oxygen, Ubuntu, Cantarell, "Fira Sans", "Droid Sans", "Helvetica Neue", sans-serif;
  max-width: 1200px;
  margin: 0 auto;
}

.logo {
  font-size: 1.2rem;
  margin-bottom: 3rem;
  color: #000;
}

.nav-grid {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 1.5rem;
  margin-bottom: 3rem;
  max-width: 400px;
}

.nav-link {
  color: #666;
  text-decoration: none;
  font-size: 1rem;
  font-weight: 400;
  transition: color 0.2s;
}

.nav-link:hover {
  color: #000;
}

.dropdown-button {
  color: #666;
  background: none;
  border: none;
  padding: 0;
  font: inherit;
  font-size: 1rem;
  cursor: pointer;
  display: flex;
  align-items: center;
  gap: 0.5rem;
}

.dropdown-button:hover {
  color: #000;
}

.dropdown-arrow {
  font-size: 1.2rem;
  transform: rotate(90deg);
  display: inline-block;
}

.status-bar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin: 2rem 0;
}

.status {
  display: flex;
  align-items: center;
  gap: 0.5rem;
}

.status-dot {
  width: 8px;
  height: 8px;
  background-color: #0070f3;
  border-radius: 50%;
}

.status-text {
  color: #0070f3;
  font-size: 1rem;
}

.tools {
  display: flex;
  gap: 0.5rem;
}

.tool-button {
  background: none;
  border: none;
  padding: 0.5rem;
  cursor: pointer;
  border-radius: 0.5rem;
  color: #666;
  display: flex;
  align-items: center;
  justify-content: center;
}

.tool-button:hover {
  background-color: #f5f5f5;
  color: #000;
}

.copyright {
  color: #666;
  font-size: 0.875rem;
  margin-top: 2rem;
}

@media (max-width: 640px) {
  .nav-grid {
    grid-template-columns: 1fr;
  }
  
  .status-bar {
    flex-direction: column;
    align-items: flex-start;
    gap: 1rem;
  }
  
  .tools {
    width: 100%;
    justify-content: flex-end;
  }
}
</style>
