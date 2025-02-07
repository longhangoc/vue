<template>
  <div class="soft-skills-template">
    <div class="template-container">
      <div class="template-content">
        <div class="content-wrapper">
          <div class="badge-container">
            <span class="trending-badge">Trending</span>
          </div>
          
          <h2 class="template-title">
            <span class="title-prefix">Exclusive</span>
            Profile Kỹ Năng Mềm
          </h2>
          
          <div class="template-info">
            <div class="features-section">
              <h3 class="section-title">Tính Năng Nổi Bật</h3>
              <div class="features-grid">
                <div 
                  v-for="(feature, index) in features" 
                  :key="index" 
                  class="feature-card"
                >
                  <div class="feature-icon-wrapper">
                    <span class="feature-icon">{{ feature.icon }}</span>
                  </div>
                  <div class="feature-details">
                    <h4 class="feature-title">{{ feature.title }}</h4>
                    <p class="feature-description">{{ feature.text }}</p>
                  </div>
                </div>
              </div>
            </div>

            <div class="pricing-section">
              <div class="price-wrapper">
                <div class="price-container">
                  <span class="original-price">140.000đ</span>
                  <span class="current-price">99.000đ</span>
                  <span class="discount-badge">-30%</span>
                </div>
              </div>
              
              <div class="cta-section">
                <a 
                  href="https://www.facebook.com/share/19U6bk7LfQ/" 
                  class="buy-now-btn"
                >
                  <span>Mua Ngay</span>
                  <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24">
                    <path d="M13 5l7 7-7 7M5 5l7 7-7 7"/>
                  </svg>
                </a>
              </div>
            </div>
          </div>
        </div>
      </div>

      <div class="template-slider-container">
        <div class="template-slider">
          <div 
            class="slider-track" 
            :style="{ transform: `translateX(-${currentSlide * 100}%)` }"
          >
            <div 
              v-for="(image, index) in images" 
              :key="index" 
              class="slide"
            >
              <div class="image-wrapper">
                <img 
                  :src="image.url" 
                  :alt="image.alt" 
                  class="slide-image"
                />
              </div>
            </div>
          </div>

          <div class="slider-controls">
            <button @click="prevSlide" class="slider-btn prev-btn">
              <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24">
                <path d="M15 18l-6-6 6-6"/>
              </svg>
            </button>
            <button @click="nextSlide" class="slider-btn next-btn">
              <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24">
                <path d="M9 18l6-6-6-6"/>
              </svg>
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'KiNangMem',
  data() {
    return {
      currentSlide: 0,
      features: [
        { 
          icon: '✨', 
          title: 'Chuyên Nghiệp',
          text: 'Thiết kế hiện đại' 
        },
        { 
          icon: '📝', 
          title: 'Tùy Biến', 
          text: 'Dễ dàng chỉnh sửa' 
        },
        { 
          icon: '🎯', 
          title: 'Trọng Tâm', 
          text: 'Đúng yêu cầu' 
        },
        { 
          icon: '⭐', 
          title: 'Bảo Đảm', 
          text: 'Bao đậu bài kiểm tra' 
        }
      ],
      images: [
        { url: 'https://i.ibb.co/C7Tm7Qj/1.png', alt: 'Template Preview 1' },
        { url: 'https://i.ibb.co/RY9mSd6/2.png', alt: 'Template Preview 2' },
        { url: 'https://i.ibb.co/HDtsKcY/3.png', alt: 'Template Preview 3' },
        { url: 'https://i.ibb.co/ySG6rd7/4.png', alt: 'Template Preview 4' },
        { url: 'https://i.ibb.co/fk3svQp/5.png', alt: 'Template Preview 5' }
      ]
    }
  },
  methods: {
    nextSlide() {
      this.currentSlide = (this.currentSlide + 1) % this.images.length;
    },
    prevSlide() {
      this.currentSlide = (this.currentSlide - 1 + this.images.length) % this.images.length;
    }
  }
}
</script>

<style scoped>
:root {
  --primary-color: #3498db;
  --text-color: #2c3e50;
  --background-color: #f0f4f8;
  --card-background: #ffffff;
}

* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

.soft-skills-template {
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
  background-color: var(--background-color);
  min-height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 1rem;
}

.template-container {
  display: flex;
  max-width: 1000px;
  width: 100%;
  background-color: var(--card-background);
  border-radius: 15px;
  box-shadow: 0 10px 25px rgba(0,0,0,0.1);
  overflow: hidden;
}

.template-content {
  flex: 1;
  padding: 2rem;
}

.badge-container {
  position: absolute;
  top: 15px;
  right: 15px;
}

.trending-badge {
  background-color: var(--primary-color);
  color: white;
  padding: 0.3rem 0.8rem;
  border-radius: 15px;
  font-size: 0.7rem;
  font-weight: 600;
}

.template-title {
  font-size: 1.8rem;
  color: var(--text-color);
  margin-bottom: 1.5rem;
  line-height: 1.2;
}

.title-prefix {
  display: block;
  font-size: 1rem;
  color: var(--primary-color);
  margin-bottom: 0.3rem;
}

.features-grid {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 0.8rem;
  margin-bottom: 1.5rem;
}

.feature-card {
  display: flex;
  align-items: center;
  background-color: #f9f9f9;
  border-radius: 10px;
  padding: 0.8rem;
}

.feature-icon-wrapper {
  background-color: rgba(52, 152, 219, 0.1);
  border-radius: 50%;
  width: 40px;
  height: 40px;
  display: flex;
  align-items: center;
  justify-content: center;
  margin-right: 0.8rem;
}

.feature-icon {
  font-size: 1.2rem;
}

.feature-title {
  font-size: 0.9rem;
  color: var(--text-color);
  margin-bottom: 0.2rem;
}

.feature-description {
  font-size: 0.8rem;
  color: #6c757d;
}

.pricing-section {
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

.price-container {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.original-price {
  text-decoration: line-through;
  color: #6c757d;
  font-size: 0.9rem;
}

.current-price {
  font-size: 1.5rem;
  color: var(--primary-color);
  font-weight: bold;
}

.discount-badge {
  background-color: #e74c3c;
  color: white;
  padding: 0.2rem 0.4rem;
  border-radius: 4px;
  font-size: 0.8rem;
}

.buy-now-btn {
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: var(--primary-color);
  color: white;
  padding: 0.8rem 1.2rem;
  text-decoration: none;
  border-radius: 10px;
  transition: all 0.3s ease;
  font-weight: 600;
  gap: 0.5rem;
}

.template-slider-container {
  flex: 1;
  position: relative;
  background-color: #f9f9f9;
}

.template-slider {
  width: 100%;
  height: 100%;
  position: relative;
  overflow: hidden;
}

.slider-track {
  display: flex;
  height: 100%;
  transition: transform 0.5s cubic-bezier(0.645, 0.045, 0.355, 1);
}

.slide {
  min-width: 100%;
  height: 100%;
}

.slide-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.slider-controls {
  position: absolute;
  top: 50%;
  left: 0;
  right: 0;
  display: flex;
  justify-content: space-between;
  transform: translateY(-50%);
  padding: 0 0.5rem;
}

.slider-btn {
  background-color: rgba(255,255,255,0.7);
  border: none;
  border-radius: 50%;
  width: 30px;
  height: 30px;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
}

.slider-btn svg {
  width: 20px;
  height: 20px;
  stroke: var(--text-color);
  stroke-width: 2;
}

@media (max-width: 768px) {
  .template-container {
    flex-direction: column;
    max-width: 100%;
    height: auto;
  }

  .template-content,
  .template-slider-container {
    flex: none;
    width: 100%;
  }

  .features-grid {
    grid-template-columns: 1fr 1fr;
  }

  .template-title {
    font-size: 1.5rem;
  }

  .slider-controls {
    display: none;
  }
}

@media (max-width: 480px) {
  .features-grid {
    grid-template-columns: 1fr;
  }

  .template-content {
    padding: 1rem;
  }

  .template-title {
    font-size: 1.3rem;
  }
}
</style>
