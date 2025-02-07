<template>
  <div class="guide">
    <h2>Hướng Dẫn Sử Dụng</h2>
    <ol>
      <li v-for="(step, index) in steps" :key="index" class="step">
        <div class="icon-wrapper">
          <!-- Sử dụng inline SVG dựa trên giá trị icon trong bước -->
          <template v-if="step.icon === 'plus'">
            <svg xmlns="http://www.w3.org/2000/svg" class="icon" width="28" height="28" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
              <line x1="12" y1="5" x2="12" y2="19"></line>
              <line x1="5" y1="12" x2="19" y2="12"></line>
            </svg>
          </template>
          <template v-else-if="step.icon === 'star'">
            <svg xmlns="http://www.w3.org/2000/svg" class="icon" width="28" height="28" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
              <polygon points="12 2 15 9 22 9 17 14 19 21 12 17 5 21 7 14 2 9 9 9"></polygon>
            </svg>
          </template>
          <template v-else-if="step.icon === 'pie'">
            <svg xmlns="http://www.w3.org/2000/svg" class="icon" width="28" height="28" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
              <path d="M21.21 15.89A10 10 0 1 1 12 2v10z"></path>
            </svg>
          </template>
          <template v-else-if="step.icon === 'download'">
            <svg xmlns="http://www.w3.org/2000/svg" class="icon" width="28" height="28" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
              <path d="M21 15v4a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2v-4"></path>
              <polyline points="7 10 12 15 17 10"></polyline>
              <line x1="12" y1="15" x2="12" y2="3"></line>
            </svg>
          </template>
        </div>
        <div class="text">
          <strong>{{ index + 1 }}. {{ step.title }}</strong>
          <p>{{ step.description }}</p>
        </div>
      </li>
    </ol>
  </div>
</template>

<script>
export default {
  name: "HuongDanSuDung",
  data() {
    return {
      steps: [
        { icon: "plus", title: "Thêm Lĩnh Vực", description: "Chọn các lĩnh vực cuộc sống để đánh giá." },
        { icon: "star", title: "Đánh Giá", description: "Cho điểm từ 1-10 cho mỗi lĩnh vực." },
        { icon: "pie", title: "Phân Tích", description: "Xem trực quan mức độ cân bằng." },
        { icon: "download", title: "Lưu Trữ", description: "Tải và theo dõi tiến trình." }
      ]
    }
  }
}
</script>

<style scoped>
.guide {
  max-width: 500px;
  margin: 20px auto;
  padding: 16px;
  font-family: 'Helvetica Neue', Arial, sans-serif;
  background: #fff;
  border-radius: 8px;
  box-shadow: 0 2px 8px rgba(0,0,0,0.1);
}
.guide h2 {
  text-align: center;
  font-size: 1.8rem;
  margin-bottom: 16px;
  color: #2c3e50;
}
ol {
  list-style: none;
  padding: 0;
  margin: 0;
}
.step {
  display: flex;
  align-items: center;
  gap: 12px;
  padding: 8px 0;
  border-bottom: 1px solid #f0f0f0;
}
.step:last-child {
  border-bottom: none;
}
.icon-wrapper {
  flex-shrink: 0;
}
.icon {
  color: #3498db;
}
.text strong {
  display: block;
  font-size: 1rem;
  color: #2c3e50;
}
.text p {
  margin: 4px 0 0;
  font-size: 0.9rem;
  color: #7f8c8d;
}
</style>
