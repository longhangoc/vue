<template>
  <div class="life-balance-guide">
    <h2 class="guide-title">
      <span class="title-icon">📚</span>
      Hướng Dẫn Sử Dụng
    </h2>
    
    <div class="steps-container">
      <div 
        v-for="(step, index) in steps" 
        :key="index" 
        class="step-item"
        :class="{ 'active': activeStep === index }"
        @mouseenter="activeStep = index"
        @mouseleave="activeStep = null"
      >
        <div class="step-icon-wrapper" :class="[step.iconClass, { 'pulse': activeStep === index }]">
          <div class="step-number">{{ index + 1 }}</div>
          <svg 
            xmlns="http://www.w3.org/2000/svg" 
            viewBox="0 0 24 24" 
            class="step-icon"
          >
            <path :d="step.iconPath" />
          </svg>
        </div>

        <div class="step-content">
          <h3 class="step-title">{{ step.title }}</h3>
          <p class="step-description">{{ step.description }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HuongDanSuDung',
  data() {
    return {
      activeStep: null,
      steps: [
        { 
          iconPath: "M12 5v14m-7-7l7-7 7 7",
          title: "Thêm Lĩnh Vực", 
          description: "Chọn các lĩnh vực cuộc sống để đánh giá.",
          iconClass: 'icon-blue'
        },
        { 
          iconPath: "M12 17.75l-6.172 3.845 1.179-6.873-5-4.867 6.9-1 3.094-6.253 3.094 6.253 6.9 1-5 4.867 1.179 6.873z",
          title: "Đánh Giá Chi Tiết", 
          description: "Đánh giá mức độ hài lòng từ 1-10 cho mỗi lĩnh vực.",
          iconClass: 'icon-purple'
        },
        { 
          iconPath: "M8 14l3 3 5-5",
          title: "Phân Tích Kết Quả", 
          description: "Xem biểu đồ trực quan về mức độ cân bằng.",
          iconClass: 'icon-green'
        },
        { 
          iconPath: "M4 16v6h16v-6M16 10l-4-4-4 4m4-4v10",
          title: "Theo Dõi & Cải Thiện", 
          description: "Lưu kết quả và theo dõi sự tiến bộ.",
          iconClass: 'icon-orange'
        }
      ]
    };
  }
}
</script>

<style scoped>
.life-balance-guide {
  max-width: 1200px;
  margin: 1rem auto;
  padding: 1.5rem;
  background: white;
  border-radius: 16px;
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.05);
}

.guide-title {
  text-align: center;
  color: #1a1a1a;
  font-size: 1.5rem;
  margin-bottom: 2rem;
  font-weight: 700;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 8px;
}

.title-icon {
  font-size: 1.6rem;
}

.steps-container {
  display: grid;
  gap: 1.5rem;
}

@media screen and (min-width: 768px) {
  .life-balance-guide {
    margin: 2rem auto;
    padding: 2rem;
  }

  .guide-title {
    font-size: 2rem;
    margin-bottom: 3rem;
  }

  .title-icon {
    font-size: 2.2rem;
  }

  .steps-container {
    grid-template-columns: repeat(4, 1fr);
    gap: 2rem;
  }
}

.step-item {
  position: relative;
  padding: 1rem;
  border-radius: 12px;
  background: white;
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
  border: 1px solid rgba(0, 0, 0, 0.05);
  display: flex;
  align-items: center;
  gap: 1rem;
}

@media screen and (min-width: 768px) {
  .step-item {
    flex-direction: column;
    align-items: flex-start;
    padding: 1.5rem;
    text-align: left;
  }

  .step-item:hover {
    transform: translateY(-5px);
    box-shadow: 0 15px 30px rgba(0, 0, 0, 0.1);
    border-color: transparent;
  }
}

.step-icon-wrapper {
  position: relative;
  display: flex;
  align-items: center;
  justify-content: center;
  width: 48px;
  height: 48px;
  border-radius: 12px;
  flex-shrink: 0;
  transition: all 0.3s ease;
}

@media screen and (min-width: 768px) {
  .step-icon-wrapper {
    width: 56px;
    height: 56px;
    margin-bottom: 1rem;
  }
}

.step-number {
  position: absolute;
  top: -6px;
  right: -6px;
  width: 20px;
  height: 20px;
  border-radius: 50%;
  background: white;
  color: #1a1a1a;
  font-weight: 600;
  font-size: 12px;
  display: flex;
  align-items: center;
  justify-content: center;
  box-shadow: 0 2px 6px rgba(0, 0, 0, 0.1);
}

.icon-blue { 
  background: linear-gradient(135deg, #60A5FA 0%, #3B82F6 100%);
  color: white;
}

.icon-purple { 
  background: linear-gradient(135deg, #A78BFA 0%, #8B5CF6 100%);
  color: white;
}

.icon-green { 
  background: linear-gradient(135deg, #34D399 0%, #10B981 100%);
  color: white;
}

.icon-orange { 
  background: linear-gradient(135deg, #FBBF24 0%, #F59E0B 100%);
  color: white;
}

.step-icon {
  width: 24px;
  height: 24px;
  stroke: currentColor;
  stroke-width: 2;
  fill: none;
}

.step-content {
  flex: 1;
}

.step-title {
  font-size: 1rem;
  color: #1a1a1a;
  margin-bottom: 0.25rem;
  font-weight: 600;
}

.step-description {
  font-size: 0.875rem;
  color: #666;
  line-height: 1.5;
}

@media screen and (min-width: 768px) {
  .step-title {
    font-size: 1.1rem;
    margin-bottom: 0.5rem;
  }

  .step-description {
    font-size: 0.95rem;
  }
}

/* Animations */
@keyframes pulse {
  0% { transform: scale(1); }
  50% { transform: scale(1.05); }
  100% { transform: scale(1); }
}

.active .step-icon-wrapper {
  transform: scale(1.1);
}

@media screen and (max-width: 768px) {
  .active .step-icon-wrapper {
    transform: scale(1.05);
  }
}
</style>
