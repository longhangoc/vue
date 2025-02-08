<template>
  <footer class="footer">
    <div class="footer-wrapper">
      <!-- Toggle Bar -->
      <div class="toggle-bar">
        <button class="toggle-item active">
          <i class="fab fa-facebook-f icon-social"></i>
        </button>
        <button class="toggle-item">
          <i class="fab fa-telegram icon-social"></i>
        </button>
      </div>

      <!-- Copyright Section -->
      <div class="footer-content">
        <p class="copyright">Copyright © {{ currentYear }} HAL Inc.</p>
        <p class="trademark">Trademark Policy</p>
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
  },
  mounted() {
    // Add click event listeners to toggle buttons
    const buttons = document.querySelectorAll('.toggle-item');
    buttons.forEach(button => {
      button.addEventListener('click', () => {
        buttons.forEach(b => b.classList.remove('active'));
        button.classList.add('active');
      });
    });
  }
}
</script>

<style scoped>
.footer {
  padding: 40px 20px;
  background: linear-gradient(to bottom, #fafafa, #f5f5f5);
  border-top: 1px solid rgba(0, 0, 0, 0.05);
}

.footer-wrapper {
  max-width: 1200px;
  margin: 0 auto;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 25px;
}

.toggle-bar {
  background: white;
  padding: 6px;
  border-radius: 40px;
  display: flex;
  gap: 8px;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.05);
  position: relative;
  transition: all 0.3s ease;
}

.toggle-bar:hover {
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.08);
  transform: translateY(-1px);
}

.toggle-item {
  width: 44px;
  height: 44px;
  border-radius: 50%;
  border: none;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  background: transparent;
  position: relative;
  transition: all 0.3s ease;
}

.toggle-item:hover {
  background: rgba(0, 0, 0, 0.03);
}

.toggle-item.active {
  background: #f0f0f0;
}

.toggle-item.active::after {
  content: '';
  position: absolute;
  bottom: -15px;
  left: 50%;
  transform: translateX(-50%);
  width: 4px;
  height: 4px;
  border-radius: 50%;
  background: #666;
}

.icon-social {
  font-size: 18px;
  color: #555;
  transition: all 0.3s ease;
}

.toggle-item:hover .icon-social {
  transform: scale(1.1);
}

.toggle-item.active .icon-social {
  color: #1a1a1a;
}

.footer-content {
  text-align: center;
  opacity: 0.9;
}

.copyright {
  font-size: 15px;
  color: #333;
  margin-bottom: 8px;
  font-weight: 500;
  letter-spacing: 0.2px;
}

.trademark {
  font-size: 15px;
  color: #666;
  letter-spacing: 0.2px;
  position: relative;
  cursor: pointer;
  display: inline-block;
}

.trademark::after {
  content: '';
  position: absolute;
  bottom: -2px;
  left: 0;
  width: 0;
  height: 1px;
  background: #666;
  transition: width 0.3s ease;
}

.trademark:hover::after {
  width: 100%;
}

/* Animation for active state */
@keyframes pulse {
  0% { transform: scale(1); }
  50% { transform: scale(1.05); }
  100% { transform: scale(1); }
}

.toggle-item.active {
  animation: pulse 0.3s ease-in-out;
}

/* Responsive Design */
@media (max-width: 768px) {
  .footer {
    padding: 30px 15px;
  }
  
  .toggle-bar {
    padding: 4px;
  }
  
  .toggle-item {
    width: 40px;
    height: 40px;
  }
  
  .icon-social {
    font-size: 16px;
  }
  
  .copyright, .trademark {
    font-size: 14px;
  }
}

/* Smooth transition for all interactive elements */
* {
  transition: all 0.2s ease-in-out;
}
</style>
