<template>
  <div class="minimalist-guide">
    <div class="guide-header">
      <h1>Hướng Dẫn Sử Dụng</h1>
    </div>

    <div class="guide-steps">
      <div 
        v-for="(step, index) in steps" 
        :key="index" 
        class="guide-step"
      >
        <div class="step-icon">
          <component :is="step.icon" />
        </div>
        <div class="step-content">
          <h3>{{ step.title }}</h3>
          <p>{{ step.description }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { 
  PlusCircleIcon, 
  StarIcon, 
  PieChartIcon, 
  DownloadIcon 
} from 'lucide-react'

export default {
  name: 'HuongDanSuDung',
  components: {
    PlusCircleIcon,
    StarIcon,
    PieChartIcon,
    DownloadIcon
  },
  data() {
    return {
      steps: [
        {
          icon: PlusCircleIcon,
          title: "Thêm Lĩnh Vực",
          description: "Chọn các lĩnh vực cuộc sống để đánh giá"
        },
        {
          icon: StarIcon,
          title: "Đánh Giá",
          description: "Cho điểm từ 1-10 cho mỗi lĩnh vực"
        },
        {
          icon: PieChartIcon,
          title: "Phân Tích",
          description: "Xem trực quan mức độ cân bằng"
        },
        {
          icon: DownloadIcon,
          title: "Lưu Trữ",
          description: "Tải và theo dõi tiến trình"
        }
      ]
    }
  }
}
</script>

<style scoped>
.minimalist-guide {
  max-width: 900px;
  margin: 0 auto;
  padding: 20px;
  background: linear-gradient(135deg, #f9fbfd, #f1f3f5);
  border-radius: 12px;
}

.guide-header {
  text-align: center;
  margin-bottom: 30px;
}

.guide-header h2 {
  font-size: 2rem;
  color: #2c3e50;
  font-weight: 600;
}

.guide-steps {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: 20px;
}

.guide-step {
  background: white;
  border-radius: 10px;
  padding: 20px;
  text-align: center;
  box-shadow: 0 5px 15px rgba(0,0,0,0.08);
  transition: transform 0.3s ease;
}

.guide-step:hover {
  transform: translateY(-5px);
}

.step-icon {
  margin-bottom: 15px;
  display: flex;
  justify-content: center;
}

.step-icon svg {
  width: 40px;
  height: 40px;
  color: #3498db;
  stroke-width: 1.5;
}

.step-content h3 {
  margin-bottom: 10px;
  color: #2c3e50;
  font-size: 1.1rem;
}

.step-content p {
  color: #7f8c8d;
  font-size: 0.9rem;
}

@media (max-width: 600px) {
  .guide-steps {
    grid-template-columns: 1fr;
  }
}
</style>
