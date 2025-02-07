<template>
  <div class="soft-skills-template">
    <div class="template-container">
      <div class="template-content">
        <div class="content-wrapper">
          <h2 class="template-title">
            <span class="title-highlight">Template</span> 
            Profile Kỹ Năng Mềm
          </h2>
          
          <div class="template-info">
            <div class="features">
              <h3>Tính năng nổi bật</h3>
              <ul class="feature-list">
                <li v-for="(feature, index) in features" :key="index">
                  <div class="feature-icon">{{ feature.icon }}</div>
                  <span class="feature-text">{{ feature.text }}</span>
                </li>
              </ul>
            </div>

            <div class="pricing">
              <div class="price-wrapper">
                <span class="original-price">140.000đ</span>
                <span class="current-price">99.000đ</span>
                <span class="discount-badge">-30%</span>
              </div>
              <a 
                href="https://www.facebook.com/share/19U6bk7LfQ/" 
                class="buy-now-btn"
              >
                Mua Ngay
              </a>
            </div>
          </div>
        </div>
      </div>

      <div class="template-slider">
        <div class="slider-container">
          <div 
            class="slider-track" 
            :style="{ transform: `translateX(-${currentSlide * 100}%)` }"
          >
            <div 
              v-for="(image, index) in images" 
              :key="index" 
              class="slide"
            >
              <img 
                :src="image.url" 
                :alt="image.alt" 
                @click="openImageModal(image)"
              />
            </div>
          </div>
        </div>

        <div class="slider-controls">
          <button @click="prevSlide" class="slider-btn prev">
            <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24">
              <path d="M15 18l-6-6 6-6"/>
            </svg>
          </button>
          <button @click="nextSlide" class="slider-btn next">
            <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24">
              <path d="M9 18l6-6-6-6"/>
            </svg>
          </button>
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
</template>

<script>
export default {
  name: 'KiNangMem',
  data() {
    return {
      currentSlide: 0,
      features: [
        { icon: '✨', text: 'Thiết kế chuyên nghiệp, hiện đại' },
        { icon: '📝', text: 'Dễ dàng chỉnh sửa và tùy biến' },
        { icon: '🎯', text: 'Đúng trọng tâm yêu cầu của giảng viên' },
        { icon: '⭐', text: 'Bao đậu bài kiểm tra số 2' }
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
  --background-color: #f9f9fc;
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
  background-color: white;
  border-radius: 16px;
  box-shadow: 0 15px 35px rgba(50,50,93,.1), 0 5px 15px rgba(0,0,0,.07);
  overflow: hidden;
}

.template-content {
  flex: 1;
  padding: 2rem;
  display: flex;
  align-items: center;
}

.content-wrapper {
  width: 100%;
}

.template-title {
  font-size: 2rem;
  color: var(--text-color);
  margin-bottom: 1.5rem;
  line-height: 1.2;
}

.title-highlight {
  color: var(--primary-color);
}

.feature-list {
  list-style: none;
  margin-bottom: 1.5rem;
}

.feature-list li {
  display: flex;
  align-items: center;
  margin-bottom: 0.75rem;
  color: #34495e;
}

.feature-icon {
  margin-right: 0.75rem;
  font-size: 1.2rem;
  width: 30px;
}

.pricing {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.price-wrapper {
  display: flex;
  align-items: center;
}

.original-price {
  text-decoration: line-through;
  color: #95a5a6;
  margin-right: 1rem;
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
  padding: 0.25rem 0.5rem;
  border-radius: 4px;
  margin-left: 0.5rem;
  font-size: 0.8rem;
}

.buy-now-btn {
  background-color: var(--primary-color);
  color: white;
  padding: 0.75rem 1.5rem;
  text-decoration: none;
  border-radius: 8px;
  transition: background-color 0.3s ease;
  font-weight: 600;
}

.buy-now-btn:hover {
  background-color: var(--secondary-color);
}

.template-slider {
  flex: 1;
  position: relative;
  overflow: hidden;
}

.slider-container {
  width: 100%;
  overflow: hidden;
}

.slider-track {
  display: flex;
  transition: transform 0.5s ease;
}

.slide {
  min-width: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
}

.slide img {
  max-width: 100%;
  height: auto;
  object-fit: cover;
  cursor: pointer;
}

.slider-controls {
  position: absolute;
  top: 50%;
  width: 100%;
  display: flex;
  justify-content: space-between;
  transform: translateY(-50%);
  padding: 0 1rem;
}

.slider-btn {
  background: rgba(255, 255, 255, 0.8);
  border: none;
  padding: 10px;
  border-radius: 50%;
  cursor: pointer;
  transition: background 0.3s ease;
  display: flex;
  align-items: center;
  justify-content: center;
}

.slider-btn svg {
  width: 24px;
  height: 24px;
  stroke: var(--primary-color);
  stroke-width: 2;
}

.slider-btn:hover {
  background: rgba(255, 255, 255, 0.9);
}

.slider-thumbnails {
  display: flex;
  justify-content: center;
  margin-top: 1rem;
  gap: 0.5rem;
}

.thumbnail {
  width: 50px;
  height: 50px;
  opacity: 0.6;
  cursor: pointer;
  transition: opacity 0.3s ease, transform 0.2s ease;
  border-radius: 8px;
  overflow: hidden;
}

.thumbnail:hover {
  transform: scale(1.1);
}

.thumbnail.active {
  opacity: 1;
  box-shadow: 0 0 0 2px var(--primary-color);
}

.thumbnail img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

@media (max-width: 768px) {
  .template-container {
    flex-direction: column-reverse;
    max-width: 100%;
  }

  .template-content {
    padding: 1rem;
  }

  .template-title {
    font-size: 1.5rem;
    text-align: center;
  }

  .template-info {
    text-align: center;
  }

  .pricing {
    flex-direction: column;
    gap: 1rem;
  }

  .slider-controls {
    display: none;
  }
}
</style>
