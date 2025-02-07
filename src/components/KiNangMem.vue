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
                <div class="price-note">Tiết kiệm 41.000đ</div>
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
                <div class="guarantee-text">
                  <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" class="shield-icon">
                    <path d="M12 22s8-4 8-10V5l-8-3-8 3v7c0 6 8 10 8 10z"/>
                  </svg>
                  Bảo hành 30 ngày
                </div>
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
                <div class="image-overlay"></div>
              </div>
            </div>
          </div>

          <div class="slider-controls">
            <button 
              @click="prevSlide" 
              class="slider-btn prev-btn"
            >
              <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24">
                <path d="M15 18l-6-6 6-6"/>
              </svg>
            </button>
            <button 
              @click="nextSlide" 
              class="slider-btn next-btn"
            >
              <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24">
                <path d="M9 18l6-6-6-6"/>
              </svg>
            </button>
          </div>

          <div class="slider-progress">
            <div 
              class="progress-bar" 
              :style="{ width: `${(currentSlide + 1) * (100 / images.length)}%` }"
            ></div>
          </div>

          <div class="slider-thumbnails">
            <div 
              v-for="(image, index) in images" 
              :key="index"
              class="thumbnail"
              :class="{ 'active': index === currentSlide }"
              @click="goToSlide(index)"
            >
              <img :src="image.url" :alt="image.alt" />
            </div>
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
          text: 'Thiết kế hiện đại, chuyên nghiệp' 
        },
        { 
          icon: '📝', 
          title: 'Tùy Biến', 
          text: 'Dễ dàng chỉnh sửa và tùy biến' 
        },
        { 
          icon: '🎯', 
          title: 'Trọng Tâm', 
          text: 'Đúng yêu cầu của giảng viên' 
        },
        { 
          icon: '⭐', 
          title: 'Bảo Đảm', 
          text: 'Bao đậu bài kiểm tra số 2' 
        }
      ],
      images: [
        { url: 'https://i.ibb.co/C7Tm7Qj/1.png', alt: 'Template Preview 1' },
        { url: 'https://i.ibb.co/RY9mSd6/2.png', alt: 'Template Preview 2' },
        { url: 'https://i.ibb.co/HDtsKcY/3.png', alt: 'Template Preview 3' },
        { url: 'https://i.ibb.co/ySG6rd7/4.png', alt: 'Template Preview 4' },
        { url: 'https://i.ibb.co/fk3svQp/5.png', alt: 'Template Preview 5' },
        { url: 'https://i.ibb.co/5890pz0/6.png', alt: 'Template Preview 6' },
        { url: 'https://i.ibb.co/mCgMnrL/7.png', alt: 'Template Preview 7' }
      ]
    }
  },
  methods: {
    nextSlide() {
      this.currentSlide = (this.currentSlide + 1) % this.images.length;
    },
    prevSlide() {
      this.currentSlide = (this.currentSlide - 1 + this.images.length) % this.images.length;
    },
    goToSlide(index) {
      this.currentSlide = index;
    }
  }
}
</script>

<style scoped>
:root {
  --primary-color: #3498db;
  --secondary-color: #2980b9;
  --text-color: #2c3e50;
  --background-color: #f0f4f8;
  --card-background: #ffffff;
  --shadow-color: rgba(50,50,93,0.1);
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
  max-width: 1200px;
  width: 100%;
  background-color: var(--card-background);
  border-radius: 20px;
  box-shadow: 
    0 25px 50px -12px var(--shadow-color), 
    0 10px 25px -5px var(--shadow-color);
  overflow: hidden;
  transform: translateY(-10px);
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.template-container:hover {
  transform: translateY(-15px);
  box-shadow: 
    0 30px 60px -15px var(--shadow-color), 
    0 15px 35px -8px var(--shadow-color);
}

.badge-container {
  position: absolute;
  top: 20px;
  right: 20px;
}

.trending-badge {
  background-color: var(--primary-color);
  color: white;
  padding: 0.5rem 1rem;
  border-radius: 20px;
  font-size: 0.8rem;
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 1px;
}

.template-content {
  flex: 1;
  padding: 3rem;
  position: relative;
  display: flex;
  align-items: center;
}

.template-title {
  font-size: 2.5rem;
  color: var(--text-color);
  margin-bottom: 2rem;
  line-height: 1.2;
}

.title-prefix {
  display: block;
  font-size: 1.2rem;
  color: var(--primary-color);
  margin-bottom: 0.5rem;
}

.features-section {
  margin-bottom: 2rem;
}

.section-title {
  font-size: 1.2rem;
  color: var(--text-color);
  margin-bottom: 1rem;
  position: relative;
}

.section-title::after {
  content: '';
  position: absolute;
  bottom: -0.5rem;
  left: 0;
  width: 50px;
  height: 3px;
  background-color: var(--primary-color);
}

.features-grid {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 1rem;
}

.feature-card {
  display: flex;
  align-items: center;
  background-color: #f9f9f9;
  border-radius: 12px;
  padding: 1rem;
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.feature-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 10px 20px -5px var(--shadow-color);
}

.feature-icon-wrapper {
  background-color: rgba(52, 152, 219, 0.1);
  border-radius: 50%;
  width: 50px;
  height: 50px;
  display: flex;
  align-items: center;
  justify-content: center;
  margin-right: 1rem;
}

.feature-icon {
  font-size: 1.5rem;
}

.feature-details {
  flex-grow: 1;
}

.feature-title {
  font-size: 1rem;
  color: var(--text-color);
  margin-bottom: 0.25rem;
}

.pricing-section {
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

.price-wrapper {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.price-container {
  display: flex;
  align-items: center;
}

.original-price {
  text-decoration: line-through;
  color: #95a5a6;
  margin-right: 1rem;
  font-size: 1rem;
}

.current-price {
  font-size: 2rem;
  color: var(--primary-color);
  font-weight: bold;
}

.discount-badge {
  background-color: #e74c3c;
  color: white;
  padding: 0.25rem 0.5rem;
  border-radius: 4px;
  margin-left: 0.5rem;
  font-size: 0.9rem;
}

.price-note {
  color: #7f8c8d;
  font-size: 0.9rem;
}

.cta-section {
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

.buy-now-btn {
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: var(--primary-color);
  color: white;
  padding: 1rem 1.5rem;
  text-decoration: none;
  border-radius: 12px;
  transition: all 0.3s ease;
  font-weight: 600;
  gap: 0.5rem;
}

.buy-now-btn:hover {
  background-color: var(--secondary-color);
  transform: translateY(-3px);
  box-shadow: 0 7px 14px rgba(50,50,93,0.1);
}

.buy-now-btn svg {
  width: 20px;
  height: 20px;
  stroke: white;
  stroke-width: 2;
}

.guarantee-text {
  display: flex;
  align-items: center;
  justify-content: center;
  color: #7f8c8d;
  font-size: 0.9rem;
  gap: 0.5rem;
}

.shield-icon {
  width: 20px;
  height: 20px;
  stroke: var(--primary-color);
  stroke-width: 2;
  fill: none;
}

.template-slider-container {
  flex: 1;
  position: relative;
  background-color: #f9f9f9;
  display: flex;
  align-items: center;
  justify-content: center;
}

.template-slider {
  width: 100%;
  position: relative;
  overflow: hidden;
}

.slider-track {
  display: flex;
  transition: transform 0.5s cubic-bezier(0.645, 0.045, 0.355, 1);
}

.slide {
  min-width: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
}

.image-wrapper {
  position: relative;
  width: 100%;
  height: 100%;
}

    .slide-image {
      width: 100%;
      height: 100%;
      object-fit: cover;
      transition: transform 0.5s ease;
    }

    .image-overlay {
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background: linear-gradient(
        to bottom, 
        rgba(0, 0, 0, 0.1), 
        rgba(0, 0, 0, 0.3)
      );
      opacity: 0.5;
      transition: opacity 0.3s ease;
    }

    .slider-controls {
      position: absolute;
      top: 50%;
      left: 0;
      right: 0;
      display: flex;
      justify-content: space-between;
      transform: translateY(-50%);
      padding: 0 1rem;
    }

    .slider-btn {
      background-color: rgba(255, 255, 255, 0.8);
      border: none;
      border-radius: 50%;
      width: 40px;
      height: 40px;
      display: flex;
      align-items: center;
      justify-content: center;
      cursor: pointer;
      transition: all 0.3s ease;
    }

    .slider-btn:hover {
      background-color: white;
      transform: scale(1.1);
    }

    .slider-btn svg {
      width: 24px;
      height: 24px;
      stroke: var(--text-color);
      stroke-width: 2;
    }

    .slider-progress {
      position: absolute;
      bottom: 20px;
      left: 20px;
      right: 20px;
      height: 4px;
      background-color: rgba(255, 255, 255, 0.3);
      border-radius: 2px;
      overflow: hidden;
    }

    .progress-bar {
      height: 100%;
      background-color: var(--primary-color);
      transition: width 0.5s ease;
    }

    .slider-thumbnails {
      position: absolute;
      bottom: 20px;
      left: 50%;
      transform: translateX(-50%);
      display: flex;
      gap: 0.5rem;
    }

    .thumbnail {
      width: 60px;
      height: 40px;
      border-radius: 8px;
      overflow: hidden;
      cursor: pointer;
      opacity: 0.6;
      transition: all 0.3s ease;
      border: 2px solid transparent;
    }

    .thumbnail.active {
      opacity: 1;
      border-color: var(--primary-color);
    }

    .thumbnail img {
      width: 100%;
      height: 100%;
      object-fit: cover;
    }

    @media (max-width: 1024px) {
      .template-container {
        flex-direction: column;
      }

      .template-content,
      .template-slider-container {
        flex: none;
        width: 100%;
      }

      .features-grid {
        grid-template-columns: 1fr;
      }
    }
  </style>
