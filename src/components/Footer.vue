<template>
  <footer class="modern-footer">
    <div class="footer-content">
      <div class="contact-buttons">
        <a href="#" class="contact-button facebook">
          <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="currentColor">
            <path d="M12 2C6.477 2 2 6.477 2 12c0 4.991 3.657 9.128 8.438 9.879V14.89h-2.54V12h2.54V9.797c0-2.506 1.492-3.89 3.777-3.89 1.094 0 2.238.195 2.238.195v2.46h-1.26c-1.243 0-1.63.771-1.63 1.562V12h2.773l-.443 2.89h-2.33v6.989C18.343 21.129 22 16.99 22 12c0-5.523-4.477-10-10-10z"/>
          </svg>
          <span>Facebook</span>
        </a>
        <a href="#" class="contact-button telegram">
          <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="currentColor">
            <path d="M12 2C6.477 2 2 6.477 2 12s4.477 10 10 10 10-4.477 10-10S17.523 2 12 2zm4.888 7.405l-1.566 7.338c-.116.511-.406.636-.822.395l-2.369-1.749-1.137 1.099c-.125.125-.23.23-.472.23l.168-2.395 4.361-3.941c.189-.168-.042-.263-.285-.094l-5.389 3.39-2.321-.724c-.504-.159-.513-.504.106-.743l9.054-3.49c.424-.153.798.105.659.739z"/>
          </svg>
          <span>Telegram</span>
        </a>
      </div>
      <div class="footer-bottom">
        <p>© {{ currentYear }} LONGHA. Đã đăng ký bản quyền.</p>
      </div>
    </div>
  </footer>
</template>

<script>
export default {
  name: 'ImprovedFooter',
  data() {
    return {
      currentYear: new Date().getFullYear()
    }
  }
}
</script>

<style scoped>
.modern-footer {
  background: linear-gradient(135deg, #f5f7fa 0%, #f2f3f7 100%);
  padding: 1.5rem;
  text-align: center;
  box-shadow: 0 -2px 10px rgba(0,0,0,0.05);
}

.footer-content {
  max-width: 600px;
  margin: 0 auto;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.contact-buttons {
  display: flex;
  justify-content: center;
  gap: 1rem;
  margin-bottom: 1.5rem;
  width: 100%;
}

.contact-button {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 0.5rem;
  padding: 12px 20px;
  border-radius: 25px;
  text-decoration: none;
  font-weight: 600;
  transition: all 0.3s ease;
  box-shadow: 0 4px 6px rgba(0,0,0,0.1);
  flex-grow: 1;
  max-width: 200px;
}

.contact-button svg {
  transition: transform 0.3s ease;
}

.contact-button:hover {
  transform: translateY(-3px);
  box-shadow: 0 6px 8px rgba(0,0,0,0.15);
}

.contact-button:hover svg {
  transform: scale(1.1);
}

.facebook {
  background-color: #1877F2;
  color: white;
}

.telegram {
  background-color: #2AABEE;
  color: white;
}

.footer-bottom {
  color: #666;
  border-top: 1px solid #e0e0e0;
  padding-top: 1rem;
  text-align: center;
  width: 100%;
}

@media (max-width: 480px) {
  .contact-buttons {
    flex-direction: column;
    align-items: stretch;
    gap: 1rem;
  }

  .contact-button {
    padding: 12px 15px;
    max-width: none;
  }

  .modern-footer {
    padding: 1rem;
  }
}
</style>
