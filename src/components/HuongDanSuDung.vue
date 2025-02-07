<template>
  <div class="life-balance-guide">
    <h2 class="guide-title">Hướng Dẫn Sử Dụng</h2>
    <div class="steps-container">
      <div 
        v-for="(step, index) in steps" 
        :key="index" 
        class="step-item"
      >
        <div class="step-icon-wrapper" :class="step.iconClass">
          <svg 
            xmlns="http://www.w3.org/2000/svg" 
            viewBox="0 0 24 24" 
            class="step-icon"
          >
            <path :d="step.iconPath" />
          </svg>
        </div>
        <div class="step-content">
          <div class="step-number">{{ index + 1 }}</div>
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
      steps: [
        { 
          iconPath: "M12 5v14m-7-7l7-7 7 7",
          title: "Thêm Lĩnh Vực", 
          description: "Chọn các lĩnh vực cuộc sống để đánh giá.",
          iconClass: 'icon-blue'
        },
        { 
          iconPath: "M12 17.75l-6.172 3.845 1.179-6.873-5-4.867 6.9-1 3.094-6.253 3.094 6.253 6.9 1-5 4.867 1.179 6.873z",
          title: "Đánh Giá", 
          description: "Cho điểm từ 1-10 cho mỗi lĩnh vực.",
          iconClass: 'icon-purple'
        },
        { 
          iconPath: "M8 14l3 3 5-5",
          title: "Phân Tích", 
          description: "Xem trực quan mức độ cân bằng.",
          iconClass: 'icon-green'
        },
        { 
          iconPath: "M4 16v6h16v-6M16 10l-4-4-4 4m4-4v10",
          title: "Lưu Trữ", 
          description: "Tải và theo dõi tiến trình.",
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
}

.guide-title {
  text-align: center;
  color: #2c3e50;
  font-size: 1.5rem;
  margin-bottom: 1.5rem;
  font-weight: 600;
}

.steps-container {
  display: flex;
  flex-direction: column;
}

@media screen and (min-width: 768px) {
  .steps-container {
    flex-direction: row;
    justify-content: space-between;
    gap: 1rem;
  }

  .step-item {
    flex-direction: column;
    align-items: center;
    text-align: center;
    flex: 1;
    border-bottom: none;
    border-right: 1px solid #f0f0f0;
    padding: 1rem;
  }

  .step-item:last-child {
    border-right: none;
  }
}

.step-item {
  display: flex;
  align-items: center;
  gap: 1rem;
  padding: 1rem 0;
  border-bottom: 1px solid #f0f0f0;
  transition: all 0.3s ease;
}

.step-item:hover {
  background-color: #f9f9f9;
}

.step-icon-wrapper {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 48px;
  height: 48px;
  border-radius: 50%;
  flex-shrink: 0;
}

.icon-blue { background-color: rgba(52, 152, 219, 0.1); color: #3498db; }
.icon-purple { background-color: rgba(155, 89, 182, 0.1); color: #9b59b6; }
.icon-green { background-color: rgba(46, 204, 113, 0.1); color: #2ecc71; }
.icon-orange { background-color: rgba(230, 126, 34, 0.1); color: #e67e22; }

.step-icon {
  width: 24px;
  height: 24px;
  stroke: currentColor;
  stroke-width: 2;
  fill: none;
}

.step-content {
  flex-grow: 1;
  position: relative;
}

@media screen and (min-width: 768px) {
  .step-content {
    text-align: center;
    margin-top: 1rem;
  }

  .step-number {
    position: static;
    margin-bottom: 0.5rem;
  }
}

.step-number {
  position: absolute;
  top: 0;
  right: 0;
  font-size: 0.8rem;
  color: #bdc3c7;
  font-weight: bold;
}

.step-title {
  font-size: 1rem;
  color: #2c3e50;
  margin-bottom: 0.25rem;
}

.step-description {
  font-size: 0.875rem;
  color: #7f8c8d;
}
</style>
