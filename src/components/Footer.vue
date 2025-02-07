<template>
  <footer class="modern-footer">
    <div class="footer-content">
      <div class="contact-buttons">
        <a href="#" class="contact-button facebook">
          <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="currentColor">
            <path d="M12 2C6.477 2 2 6.477 2 12c0 4.991 3.657 9.128 8.438 9.879V14.89h-2.54V12h2.54V9.797c0-2.506 1.492-3.89 3.777-3.89 1.094 0 2.238.195 2.238.195v2.46h-1.26c-1.243 0-1.63.771-1.63 1.562V12h2.773l-.443 2.89h-2.33v6.989C18.343 21.129 22 16.99 22 12c0-5.523-4.477-10-10-10z"/>
          </svg>
          Facebook
        </a>
        <a href="#" class="contact-button telegram">
          <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="currentColor">
            <path d="M12 2C6.477 2 2 6.477 2 12s4.477 10 10 10 10-4.477 10-10S17.523 2 12 2zm4.888 7.405l-1.566 7.338c-.116.511-.406.636-.822.395l-2.369-1.749-1.137 1.099c-.125.125-.23.23-.472.23l.168-2.395 4.361-3.941c.189-.168-.042-.263-.285-.094l-5.389 3.39-2.321-.724c-.504-.159-.513-.504.106-.743l9.054-3.49c.424-.153.798.105.659.739z"/>
          </svg>
          Telegram
        </a>
        <a href="#" class="contact-button zalo">
          <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="currentColor">
            <path d="M14.414 5H9.586a1 1 0 0 0-1 1v11.414l2.293-2.293a1 1 0 0 1 1.414 0L14 17.414V6a1 1 0 0 0-1-1zm-2.828-2h4.242a3 3 0 0 1 3 3v13a1 1 0 0 1-1.707.707L12 16.414l-5.121 5.293A1 1 0 0 1 5.172 21v-13a3 3 0 0 1 3-3z"/>
          </svg>
          Zalo
        </a>
      </div>
      <div class="footer-bottom">
        <p>© {{ currentYear }} LONGHA.</p>
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
.modern-footer {
  background: linear-gradient(135deg, #f5f7fa 0%, #f2f3f7 100%);
  padding: 2rem;
  text-align: center;
}

.footer-content {
  max-width: 800px;
  margin: 0 auto;
}

.contact-buttons {
  display: flex;
  justify-content: center;
  gap: 1.5rem;
  margin-bottom: 1.5rem;
}

.contact-button {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 0.5rem;
  padding: 10px 20px;
  border-radius: 30px;
  text-decoration: none;
  font-weight: 600;
  transition: all 0.3s ease;
  box-shadow: 0 4px 6px rgba(0,0,0,0.1);
}

.contact-button svg {
  transition: transform 0.3s ease;
}

.contact-button:hover {
  transform: translateY(-5px);
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

.zalo {
  background-color: #0068FF;
  color: white;
}

.footer-bottom {
  color: #666;
  border-top: 1px solid #e0e0e0;
  padding-top: 1rem;
}

@media (max-width: 768px) {
  .contact-buttons {
    flex-direction: column;
    gap: 1rem;
  }

  .contact-button {
    width: 100%;
  }
}
</style>
