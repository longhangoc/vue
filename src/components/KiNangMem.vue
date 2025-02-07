<template>
  <div class="soft-skills-template">
    <div class="template-container">
      <div class="template-content">
        <h2 class="template-title">Template Profile Kỹ Năng Mềm</h2>
        
        <div class="template-info">
          <div class="features">
            <h3>Tính năng nổi bật:</h3>
            <ul class="feature-list">
              <li>
                <span class="feature-icon">✨</span>
                Thiết kế chuyên nghiệp, hiện đại
              </li>
              <li>
                <span class="feature-icon">📝</span>
                Dễ dàng chỉnh sửa và tùy biến
              </li>
              <li>
                <span class="feature-icon">🎯</span>
                Đúng trọng tâm yêu cầu của giảng viên
              </li>
              <li>
                <span class="feature-icon">⭐</span>
                Bao đậu bài kiểm tra số 2
              </li>
            </ul>
          </div>

          <div class="pricing">
            <div class="price-container">
              <span class="original-price">140.000đ</span>
              <span class="current-price">99.000đ</span>
            </div>
            <a href="https://www.facebook.com/share/19U6bk7LfQ/" class="buy-now-btn">
              Mua Ngay
            </a>
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
              <img :src="image.url" :alt="image.alt" />
            </div>
          </div>
        </div>

        <div class="slider-controls">
          <button @click="prevSlide" class="slider-btn prev">❮</button>
          <button @click="nextSlide" class="slider-btn next">❯</button>
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
.soft-skills-template {
  font-family: 'Inter', sans-serif;
  max-width: 1200px;
  margin: 0 auto;
  padding: 2rem;
  background-color: #f9f9fc;
}

.template-container {
  display: flex;
  align-items: center;
  gap: 2rem;
  background-color: white;
  border-radius: 16px;
  box-shadow: 0 10px 25px rgba(0, 0, 0, 0.1);
  overflow: hidden;
}

.template-content {
  flex: 1;
  padding: 2rem;
}

.template-title {
  font-size: 2rem;
  color: #2c3e50;
  margin-bottom: 1.5rem;
  font-weight: 700;
}

.feature-list {
  list-style: none;
  padding: 0;
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
}

.pricing {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-top: 1.5rem;
}

.price-container {
  display: flex;
  align-items: center;
}

.original-price {
  text-decoration: line-through;
  color: #95a5a6;
  margin-right: 1rem;
}

.current-price {
  font-size: 1.5rem;
  color: #e74c3c;
  font-weight: bold;
}

.buy-now-btn {
  background-color: #3498db;
  color: white;
  padding: 0.75rem 1.5rem;
  text-decoration: none;
  border-radius: 8px;
  transition: background-color 0.3s ease;
}

.buy-now-btn:hover {
  background-color: #2980b9;
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
}

.slider-controls {
  position: absolute;
  top: 50%;
  width: 100%;
  display: flex;
  justify-content: space-between;
  transform: translateY(-50%);
}

.slider-btn {
  background: rgba(255, 255, 255, 0.7);
  border: none;
  padding: 10px 15px;
  border-radius: 50%;
  cursor: pointer;
  transition: background 0.3s ease;
}

.slider-btn:hover {
  background: rgba(255, 255, 255, 0.9);
}

.slider-thumbnails {
  display: flex;
  justify-content: center;
  margin-top: 1rem;
}

.thumbnail {
  width: 60px;
  height: 60px;
  margin: 0 0.5rem;
  opacity: 0.6;
  cursor: pointer;
  transition: opacity 0.3s ease;
}

.thumbnail.active {
  opacity: 1;
  border: 2px solid #3498db;
}

.thumbnail img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

@media (max-width: 768px) {
  .template-container {
    flex-direction: column;
  }
}
</style>
