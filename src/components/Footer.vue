<template>
  <footer class="footer">
    <div class="footer-wrapper">
      <!-- Social Media Bar -->
      <div class="social-bar">
        <a href="https://www.facebook.com/share/1BSHU3XjFW/" target="_blank" class="social-item" aria-label="Facebook">
          <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 320 512" class="social-icon">
            <path d="M279.14 288l14.22-92.66h-88.91v-60.13c0-25.35 12.42-50.06 52.24-50.06h40.42V6.26S260.43 0 225.36 0c-73.22 0-121.08 44.38-121.08 124.72v70.62H22.89V288h81.39v224h100.17V288z"/>
          </svg>
        </a>
        <a href="https://t.me/longha102/" target="_blank" class="social-item" aria-label="Telegram">
          <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 496 512" class="social-icon">
            <path d="M248,8C111.033,8,0,119.033,0,256S111.033,504,248,504,496,392.967,496,256,384.967,8,248,8ZM362.952,176.66c-3.732,39.215-19.881,134.378-28.1,178.3-3.476,18.584-10.322,24.816-16.948,25.425-14.4,1.326-25.338-9.517-39.287-18.661-21.827-14.308-34.158-23.215-55.346-37.177-24.485-16.135-8.612-25,5.342-39.5,3.652-3.793,67.107-61.51,68.335-66.746.153-.655.3-3.1-1.154-4.384s-3.59-.849-5.135-.5q-3.283.746-104.608,69.142-14.845,10.194-26.894,9.934c-8.855-.191-25.888-5.006-38.551-9.123-15.531-5.048-27.875-7.717-26.8-16.291q.84-6.7,18.45-13.7,108.446-47.248,144.628-62.3c68.872-28.647,83.183-33.623,92.511-33.789,2.052-.034,6.639.474,9.61,2.885a10.452,10.452,0,0,1,3.53,6.716A43.765,43.765,0,0,1,362.952,176.66Z"/>
          </svg>
        </a>
      </div>

      <!-- Copyright Section -->
      <div class="footer-content">
        <p class="copyright">Copyright © {{ currentYear }} HAL.</p>
        <p class="trademark">From Long Hà with love ❤️</p>
      </div>
    </div>
  </footer>
</template>

<script>
export default {
  name: 'PhanDitFooter',
  computed: {
    currentYear() {
      return new Date().getFullYear();
    }
  }
}
</script>

<style scoped>
.footer {
  padding: 40px 20px;
  background: linear-gradient(to bottom, #ffffff, #fafafa);
  border-top: 1px solid rgba(0, 0, 0, 0.06);
}

.footer-wrapper {
  max-width: 1200px;
  margin: 0 auto;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 30px;
}

.social-bar {
  background: white;
  padding: 8px;
  border-radius: 40px;
  display: flex;
  gap: 12px;
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.06);
  position: relative;
  transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
}

.social-bar:hover {
  box-shadow: 0 6px 25px rgba(0, 0, 0, 0.08);
  transform: translateY(-2px);
}

.social-item {
  width: 48px;
  height: 48px;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  background: transparent;
  position: relative;
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
  cursor: pointer;
}

.social-item::before {
  content: '';
  position: absolute;
  inset: 0;
  border-radius: 50%;
  background: currentColor;
  opacity: 0;
  transition: opacity 0.3s ease;
}

.social-item:hover::before {
  opacity: 0.06;
}

.social-item:active {
  transform: scale(0.95);
}

.social-icon {
  width: 20px;
  height: 20px;
  fill: #444;
  transition: all 0.3s ease;
}

.social-item:hover .social-icon {
  fill: #1a1a1a;
  transform: scale(1.1);
}

.footer-content {
  text-align: center;
  opacity: 0.9;
}

.copyright {
  font-size: 15px;
  color: #333;
  margin-bottom: 10px;
  font-weight: 500;
  letter-spacing: 0.3px;
}

.trademark {
  font-size: 15px;
  color: #666;
  letter-spacing: 0.3px;
  position: relative;
  cursor: pointer;
  display: inline-block;
  transition: all 0.3s ease;
}

.trademark::after {
  content: '';
  position: absolute;
  bottom: -2px;
  left: 0;
  width: 0;
  height: 1px;
  background: #666;
  transition: width 0.4s cubic-bezier(0.4, 0, 0.2, 1);
}

.trademark:hover {
  color: #333;
}

.trademark:hover::after {
  width: 100%;
}

/* Smooth hover effect for social icons */
@keyframes socialHover {
  0% { transform: translateY(0); }
  50% { transform: translateY(-2px); }
  100% { transform: translateY(0); }
}

.social-item:hover {
  animation: socialHover 0.6s cubic-bezier(0.4, 0, 0.2, 1);
}

/* Responsive Design */
@media (max-width: 768px) {
  .footer {
    padding: 30px 15px;
  }
  
  .social-bar {
    padding: 6px;
  }
  
  .social-item {
    width: 44px;
    height: 44px;
  }
  
  .social-icon {
    width: 18px;
    height: 18px;
  }
  
  .copyright, .trademark {
    font-size: 14px;
  }
}

/* High-DPI Screen Optimizations */
@media (-webkit-min-device-pixel-ratio: 2), (min-resolution: 192dpi) {
  .social-bar {
    box-shadow: 0 4px 16px rgba(0, 0, 0, 0.05);
  }
}
</style>
