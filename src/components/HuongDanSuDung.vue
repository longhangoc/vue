<template>
  <div class="guide">
    <h2>Hướng Dẫn Sử Dụng</h2>
    <ol>
      <li v-for="(step, index) in steps" :key="index">
        <strong>{{ index + 1 }}. {{ step.title }}</strong>
        <p>{{ step.description }}</p>
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
        { title: "Thêm Lĩnh Vực", description: "Chọn các lĩnh vực cuộc sống để đánh giá." },
        { title: "Đánh Giá", description: "Cho điểm từ 1-10 cho mỗi lĩnh vực." },
        { title: "Phân Tích", description: "Xem trực quan mức độ cân bằng." },
        { title: "Lưu Trữ", description: "Tải và theo dõi tiến trình." }
      ]
    }
  }
}
</script>

<style scoped>
.guide {
  max-width: 500px;
  margin: 20px auto;
  padding: 10px;
  font-family: sans-serif;
}
.guide h2 {
  text-align: center;
  font-size: 1.5rem;
  margin-bottom: 10px;
}
.guide ol {
  padding-left: 20px;
}
.guide li {
  margin-bottom: 10px;
}
.guide li p {
  margin: 0;
  font-size: 0.9rem;
  color: #555;
}
</style>
