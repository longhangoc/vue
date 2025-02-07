<template>
  <div class="enhanced-guide-container">
    <h2 class="section-title">
      <svg xmlns="http://www.w3.org/2000/svg" width="40" height="40" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="title-icon">
        <path d="M12 20h9"></path>
        <path d="M16.5 3.5a2.121 2.121 0 0 1 3 3L7 19l-4 1 1-4L16.5 3.5z"></path>
      </svg>
      Hướng Dẫn Sử Dụng
    </h2>

    <div class="guide-steps">
      <div class="guide-step" v-for="(step, index) in steps" :key="index">
        <div class="step-icon-container">
          <component :is="step.icon" class="step-icon"></component>
        </div>
        <div class="step-content">
          <div class="step-number">{{ index + 1 }}</div>
          <h3>{{ step.title }}</h3>
          <p>{{ step.description }}</p>
        </div>
      </div>
    </div>

    <div class="guide-tips">
      <h3>
        <svg xmlns="http://www.w3.org/2000/svg" width="32" height="32" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-lienjoin="round" class="tips-icon">
          <path d="M12 20h9"></path>
          <path d="M16.5 3.5a2.121 2.121 0 0 1 3 3L7 19l-4 1 1-4L16.5 3.5z"></path>
        </svg>
        Lời Khuyên
      </h3>
      <ul>
        <li v-for="(tip, index) in tips" :key="index">
          <span class="tip-icon">✓</span>
          {{ tip }}
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import { 
  PlusCircleIcon, 
  StarIcon, 
  ChartPieIcon, 
  DownloadIcon 
} from 'lucide-react'

export default {
  name: "HuongDan",
  components: {
    PlusCircleIcon,
    StarIcon,
    ChartPieIcon,
    DownloadIcon
  },
  data() {
    return {
      steps: [
        {
          icon: PlusCircleIcon,
          title: "Thêm Lĩnh Vực",
          description: "Nhấn vào nút \"Thêm lĩnh vực\" để bổ sung các khía cạnh cuộc sống bạn muốn đánh giá."
        },
        {
          icon: StarIcon,
          title: "Đánh Giá Điểm Số",
          description: "Cho điểm từ 1-10 cho mỗi lĩnh vực, phản ánh mức độ hài lòng của bạn."
        },
        {
          icon: ChartPieIcon,
          title: "Xem Kết Quả",
          description: "Bánh xe sẽ hiển thị trực quan mức độ cân bằng trong cuộc sống của bạn."
        },
        {
          icon: DownloadIcon,
          title: "Lưu Kết Quả",
          description: "Tải về dưới dạng SVG hoặc PNG để theo dõi sự tiến bộ của bản thân."
        }
      ],
      tips: [
        "Hãy trung thực trong đánh giá",
        "Đánh giá định kỳ mỗi tháng",
        "Tập trung cải thiện các điểm thấp",
        "Duy trì các lĩnh vực đã tốt"
      ]
    }
  }
}
</script>

<style scoped>
.enhanced-guide-container {
  background: linear-gradient(135deg, #f5f7fa 0%, #f2f3f7 100%);
  padding: 40px 20px;
  border-radius: 15px;
  max-width: 1200px;
  margin: 20px auto;
  box-shadow: 0 10px 25px rgba(0,0,0,0.1);
}

.section-title {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 15px;
  text-align: center;
  font-size: 2.5rem;
  margin-bottom: 40px;
  color: #2c3e50;
  font-weight: 700;
}

.title-icon, .tips-icon {
  color: #3498db;
  stroke-width: 2;
}

.guide-steps {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 20px;
  margin-bottom: 40px;
}

.guide-step {
  background: white;
  border-radius: 15px;
  padding: 25px;
  text-align: center;
  box-shadow: 0 8px 15px rgba(0,0,0,0.1);
  transition: all 0.3s ease;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.guide-step:hover {
  transform: translateY(-10px);
  box-shadow: 0 12px 20px rgba(0,0,0,0.15);
}

.step-icon-container {
  margin-bottom: 20px;
}

.step-icon {
  width: 60px;
  height: 60px;
  color: #3498db;
  stroke-width: 1.5;
}

.step-number {
  width: 45px;
  height: 45px;
  border-radius: 50%;
  background: linear-gradient(135deg, #6a11cb 0%, #2575fc 100%);
  color: white;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 1.2rem;
  font-weight: bold;
  margin-bottom: 15px;
}

.guide-step h3 {
  color: #2c3e50;
  margin-bottom: 10px;
  font-size: 1.2rem;
}

.guide-step p {
  color: #7f8c8d;
  line-height: 1.6;
}

.guide-tips {
  background: white;
  border-radius: 15px;
  padding: 30px;
  box-shadow: 0 8px 15px rgba(0,0,0,0.1);
  text-align: center;
}

.guide-tips h3 {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 15px;
  margin-bottom: 25px;
  color: #2c3e50;
  font-size: 2rem;
}

.guide-tips ul {
  list-style: none;
  padding: 0;
  display: flex;
  flex-direction: column;
  gap: 15px;
}

.guide-tips li {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 10px;
  color: #34495e;
  font-size: 1rem;
}

.tip-icon {
  color: #2ecc71;
  font-weight: bold;
}

@media (max-width: 768px) {
  .section-title {
    font-size: 2rem;
  }

  .guide-steps {
    grid-template-columns: 1fr;
  }
}
</style>
