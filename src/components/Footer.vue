<template>
  <footer class="footer">
    <div class="footer-content">
      <p class="copyright">
        © {{ currentYear }} HAL.
      </p>
      <div class="social-links">
        <a href="#" class="social-link">
          <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
            <path d="M18 2h-3a5 5 0 0 0-5 5v3H7v4h3v8h4v-8h3l1-4h-4V7a1 1 0 0 1 1-1h3z"></path>
          </svg>
        </a>
        <a href="#" class="social-link">
          <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
            <rect x="2" y="2" width="20" height="20" rx="5" ry="5"></rect>
            <path d="M16 11.37A4 4 0 1 1 12.63 8 4 4 0 0 1 16 11.37z"></path>
            <line x1="17.5" y1="6.5" x2="17.51" y2="6.5"></line>
          </svg>
        </a>
        <a href="#" class="social-link">
          <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
            <path d="M23 3a10.9 10.9 0 0 1-3.14 1.53 4.48 4.48 0 0 0-7.86 3v1A10.66 10.66 0 0 1 3 4s-4 9 5 13a11.64 11.64 0 0 1-7 2c9 5 20 0 20-11.5a4.5 4.5 0 0 0-.08-.83A7.72 7.72 0 0 0 23 3z"></path>
          </svg>
        </a>
      </div>
    </div>
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
  background-color: #111;
  color: #ccc;
  padding: 2rem 1.5rem;
  text-align: center;
  position: relative;
  overflow: hidden;
}

.footer-content {
  max-width: 1200px;
  margin: 0 auto;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 1.5rem;
}

.copyright {
  font-size: 0.9rem;
  opacity: 0.8;
  letter-spacing: 0.05em;
}

.social-links {
  display: flex;
  gap: 2rem;
}

.social-link {
  color: #fff;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  width: 2.5rem;
  height: 2.5rem;
  border-radius: 50%;
  background-color: rgba(255,255,255,0.1);
  transition: all 0.3s ease;
}

.social-link svg {
  width: 1.5rem;
  height: 1.5rem;
  stroke: currentColor;
}

.social-link:hover {
  background-color: #2575fc;
  color: white;
  transform: scale(1.1) rotate(6deg);
}

@media (max-width: 768px) {
  .social-links {
    gap: 1.5rem;
  }

  .social-link {
    width: 2rem;
    height: 2rem;
  }

  .social-link svg {
    width: 1.2rem;
    height: 1.2rem;
  }
}
</style>
