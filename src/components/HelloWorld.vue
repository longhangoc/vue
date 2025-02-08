<template>
  <div class="life-wheel-container">
    <header class="wheel-header">
  
    </header>

    <div class="content">
      <!-- Controls Panel -->
      <section class="controls-panel">
        <div class="panel-header">
          
          <button @click="addArea" class="btn-secondary" :disabled="areas.length >= 12">
            <span class="btn-icon">+</span> Thêm lĩnh vực
          </button>
        </div>

        <div class="areas-container">
          <TransitionGroup name="list" tag="div" class="area-list">
            <div v-for="(area, i) in areas" :key="i" class="area-card">
              <div class="area-header">
                <div class="color-indicator" :style="{ backgroundColor: area.color }"></div>
                <input
                  type="text"
                  class="area-name-input"
                  v-model="area.name"
                  @input="updateArea(i, 'name', $event.target.value)"
                  placeholder="Tên lĩnh vực"
                />
                <button class="btn-icon-remove" @click="removeArea(i)" :disabled="areas.length <= 3">
                  ×
                </button>
              </div>
              
              <div class="area-controls">
                <div class="value-control">
                  <span class="value-label">Mức độ: {{ area.value }}/10</span>
                  <input
                    type="range"
                    class="slider"
                    min="0"
                    max="10"
                    v-model.number="area.value"
                    @input="updateArea(i, 'value', parseInt($event.target.value))"
                  />
                </div>
                <input
                  type="color"
                  class="color-picker"
                  v-model="area.color"
                  @input="updateArea(i, 'color', $event.target.value)"
                  title="Chọn màu"
                />
              </div>
            </div>
          </TransitionGroup>
        </div>

        <div class="action-buttons">
          <button @click="saveAsSVG" class="btn-secondary">
            <span class="btn-icon">↓</span> Tải SVG
          </button>
          <button @click="saveAsPNG" class="btn-secondary">
            <span class="btn-icon">↓</span> Tải PNG
          </button>
        </div>
      </section>

      <!-- Wheel Display -->
      <section class="wheel-display">
        <div class="wheel-container">
          <svg id="wheel" viewBox="0 0 500 500" ref="wheelSvg" class="life-wheel"></svg>
        </div>
      </section>
    </div>
  </div>
</template>

<script>
export default {
  name: 'LifeWheel',
  data() {
    return {
      areas: [
        { name: "SỰ NGHIỆP", value: 7, color: "#e74c3c" },
        { name: "TÀI CHÍNH", value: 6, color: "#2ecc71" },
        { name: "SỨC KHỎE", value: 8, color: "#3498db" },
        { name: "GIA ĐÌNH", value: 5, color: "#95a5a6" },
        { name: "CÁC MỐI QUAN HỆ", value: 7, color: "#f1c40f" },
        { name: "SỰ HOÀN THIỆN", value: 6, color: "#f39c12" },
        { name: "GIẢI TRÍ", value: 8, color: "#1abc9c" },
        { name: "TÂM LINH", value: 7, color: "#9b59b6" }
      ]
    }
  },
  methods: {
    updateArea(index, property, value) {
      this.areas[index][property] = value;
      this.drawWheel();
      if (property === 'value') {
        this.$nextTick(() => {
          this.updateSliderBackground(document.querySelectorAll('.slider')[index]);
        });
      }
    },
    addArea() {
      const colors = ["#e74c3c", "#2ecc71", "#3498db", "#95a5a6", "#f1c40f", "#f39c12", "#1abc9c", "#9b59b6"];
      this.areas.push({
        name: "Lĩnh vực mới",
        value: 5,
        color: colors[Math.floor(Math.random() * colors.length)]
      });
      this.drawWheel();
      this.$nextTick(() => {
        this.initializeSliders();
      });
    },
    removeArea(index) {
      if (this.areas.length > 3) {
        this.areas.splice(index, 1);
        this.drawWheel();
        this.$nextTick(() => {
          this.initializeSliders();
        });
      }
    },
    initializeSliders() {
      const sliders = document.querySelectorAll('.slider');
      sliders.forEach(slider => {
        this.updateSliderBackground(slider);
        slider.addEventListener('input', (e) => {
          this.updateSliderBackground(e.target);
        });
      });
    },
    updateSliderBackground(slider) {
      const value = ((slider.value - slider.min) / (slider.max - slider.min)) * 100;
      slider.style.backgroundSize = `${value}% 100%`;
    },
    drawWheel() {
      const svg = this.$refs.wheelSvg;
      const centerX = 250;
      const centerY = 250;
      const maxRadius = 200;
      const outerRadius = maxRadius + 40;
      svg.innerHTML = '';

      const defs = document.createElementNS("http://www.w3.org/2000/svg", "defs");
      svg.appendChild(defs);

      // Vẽ các vòng tròn đồng tâm và số vòng
      for (let i = 1; i <= 10; i++) {
        const circle = document.createElementNS("http://www.w3.org/2000/svg", "circle");
        circle.setAttribute("cx", centerX);
        circle.setAttribute("cy", centerY);
        circle.setAttribute("r", maxRadius * i / 10);
        circle.setAttribute("fill", "none");
        circle.setAttribute("stroke", "#e9ecef");
        circle.setAttribute("stroke-width", "1");
        svg.appendChild(circle);

        const text = document.createElementNS("http://www.w3.org/2000/svg", "text");
        text.setAttribute("x", centerX - 15);
        text.setAttribute("y", centerY - (maxRadius * i / 10) + 15);
        text.setAttribute("fill", "#95a5a6");
        text.setAttribute("font-size", "12px");
        text.textContent = i;
        svg.appendChild(text);
      }

      const angleStep = (2 * Math.PI) / this.areas.length;
      this.areas.forEach((area, i) => {
        const startAngle = i * angleStep - Math.PI / 2;
        const endAngle = (i + 1) * angleStep - Math.PI / 2;
        const midAngle = (startAngle + endAngle) / 2;

        // Vẽ đường phân cách
        const x2 = centerX + maxRadius * Math.cos(startAngle);
        const y2 = centerY + maxRadius * Math.sin(startAngle);
        const line = document.createElementNS("http://www.w3.org/2000/svg", "line");
        line.setAttribute("x1", centerX.toString());
        line.setAttribute("y1", centerY.toString());
        line.setAttribute("x2", x2.toString());
        line.setAttribute("y2", y2.toString());
        line.setAttribute("stroke", "#000");
        line.setAttribute("stroke-width", "2");
        svg.appendChild(line);

        // Vẽ viền ngoài
        const x1 = centerX + maxRadius * Math.cos(startAngle);
        const y1 = centerY + maxRadius * Math.sin(startAngle);
        const x2End = centerX + maxRadius * Math.cos(endAngle);
        const y2End = centerY + maxRadius * Math.sin(endAngle);
        const x3 = centerX + outerRadius * Math.cos(endAngle);
        const y3 = centerY + outerRadius * Math.sin(endAngle);
        const x4 = centerX + outerRadius * Math.cos(startAngle);
        const y4 = centerY + outerRadius * Math.sin(startAngle);

        const outerArc = document.createElementNS("http://www.w3.org/2000/svg", "path");
        const outerD = `M ${x1} ${y1} A ${maxRadius} ${maxRadius} 0 0 1 ${x2End} ${y2End} L ${x3} ${y3} A ${outerRadius} ${outerRadius} 0 0 0 ${x4} ${y4} Z`;
        outerArc.setAttribute("d", outerD);
        outerArc.setAttribute("fill", area.color);
        outerArc.setAttribute("stroke", "#000");
        outerArc.setAttribute("stroke-width", "2");
        svg.appendChild(outerArc);

        // Text path
        const pathId = `textPath${i}`;
        const textRadius = maxRadius + 20;
        const isBottomHalf = midAngle > 0 && midAngle < Math.PI;
        let pathStart, pathEnd;

        if (isBottomHalf) {
          pathStart = {
            x: centerX + textRadius * Math.cos(endAngle),
            y: centerY + textRadius * Math.sin(endAngle)
          };
          pathEnd = {
            x: centerX + textRadius * Math.cos(startAngle),
            y: centerY + textRadius * Math.sin(startAngle)
          };
        } else {
          pathStart = {
            x: centerX + textRadius * Math.cos(startAngle),
            y: centerY + textRadius * Math.sin(startAngle)
          };
          pathEnd = {
            x: centerX + textRadius * Math.cos(endAngle),
            y: centerY + textRadius * Math.sin(endAngle)
          };
        }

        const path = document.createElementNS("http://www.w3.org/2000/svg", "path");
        path.setAttribute("id", pathId);
        path.setAttribute("d", `M ${pathStart.x} ${pathStart.y} A ${textRadius} ${textRadius} 0 0 ${isBottomHalf ? 0 : 1} ${pathEnd.x} ${pathEnd.y}`);
        path.setAttribute("fill", "none");
        defs.appendChild(path);

        const textEl = document.createElementNS("http://www.w3.org/2000/svg", "text");
        textEl.setAttribute("fill", "#fff");
        textEl.setAttribute("font-size", "12px");
        textEl.setAttribute("font-weight", "bold");

        const textPathElement = document.createElementNS("http://www.w3.org/2000/svg", "textPath");
        textPathElement.setAttributeNS("http://www.w3.org/1999/xlink", "xlink:href", `#${pathId}`);
        textPathElement.setAttribute("startOffset", "50%");
        textPathElement.setAttribute("text-anchor", "middle");
        textPathElement.textContent = area.name;
        textEl.appendChild(textPathElement);
        svg.appendChild(textEl);

        // Vẽ phần value
        const radius = maxRadius * (area.value / 10);
        const valueX1 = centerX + radius * Math.cos(startAngle);
        const valueY1 = centerY + radius * Math.sin(startAngle);
        const valueX2 = centerX + radius * Math.cos(endAngle);
        const valueY2 = centerY + radius * Math.sin(endAngle);

        const valuePath = document.createElementNS("http://www.w3.org/2000/svg", "path");
        const valueD = `M ${centerX} ${centerY} L ${valueX1} ${valueY1} A ${radius} ${radius} 0 0 1 ${valueX2} ${valueY2} Z`;
        valuePath.setAttribute("d", valueD);
        valuePath.setAttribute("fill", area.color);
        valuePath.setAttribute("stroke", "#000");
        valuePath.setAttribute("stroke-width", "2");
        valuePath.setAttribute("fill-opacity", "0.7");
        svg.appendChild(valuePath);
      });
    },
    saveAsSVG() {
      const svg = this.$refs.wheelSvg;
      const serializer = new XMLSerializer();
      const source = serializer.serializeToString(svg);
      const blob = new Blob([source], { type: 'image/svg+xml' });
      const url = URL.createObjectURL(blob);
      const a = document.createElement('a');
      a.href = url;
      a.download = 'banh-xe-cuoc-doi.svg';
      document.body.appendChild(a);
      a.click();
      document.body.removeChild(a);
      URL.revokeObjectURL(url);
    },
    saveAsPNG() {
      const svg = this.$refs.wheelSvg;
      const serializer = new XMLSerializer();
      const source = serializer.serializeToString(svg);
      const canvas = document.createElement('canvas');
      const ctx = canvas.getContext('2d');

      const scaleFactor = 10;
      const width = 500 * scaleFactor;
      const height = 500 * scaleFactor;

      canvas.width = width;
      canvas.height = height;

      const img = new Image();
      img.onload = () => {
        ctx.drawImage(img, 0, 0, width, height);
        const pngUrl = canvas.toDataURL('image/png', 1.0);
        const a = document.createElement('a');
        a.href = pngUrl;
        a.download = 'banh-xe-cuoc-doi.png';
        document.body.appendChild(a);
        a.click();
        document.body.removeChild(a);
      };

      img.src = 'data:image/svg+xml;charset=utf-8;base64,' + btoa(unescape(encodeURIComponent(source)));
    }
  },
  mounted() {
    this.drawWheel();
    this.initializeSliders();
  },
  watch: {
    areas: {
      deep: true,
      handler() {
        this.drawWheel();
      }
    }
  }
}
</script>

<style scoped>
   :root {
  --primary-color: #6366f1;
  --primary-hover: #4f46e5;
  --secondary-color: #64748b;
  --danger-color: #dc2626;
  --text-color: #334155;
  --border-color: #e2e8f0;
  --bg-subtle: #f8fafc;
  --border-radius: 12px;
  --shadow-sm: 0 2px 4px rgba(0,0,0,0.03);
  --shadow-md: 0 4px 6px rgba(0,0,0,0.05);
  --shadow-lg: 0 10px 15px rgba(0,0,0,0.08);
}

.life-wheel-container {
  max-width: 1200px;
  margin: 0 auto;
  padding: clamp(10px, 2vw, 20px);
  background: linear-gradient(150deg, #ffffff, var(--bg-subtle));
  min-height: 100vh;
}

.wheel-header {
  text-align: center;
  margin-bottom: clamp(1rem, 3vw, 2rem);
  padding: clamp(1rem, 3vw, 2rem) 0;
}

.text-gradient {
  font-size: clamp(2rem, 4vw, 3rem);
  background: linear-gradient(135deg, #6366f1, #818cf8);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  margin-bottom: 0.5rem;
}

.controls-panel {
  background: white;
  border-radius: var(--border-radius);
  padding: clamp(1.25rem, 2vw, 1.75rem);
  box-shadow: var(--shadow-md);
  border: 1px solid var(--border-color);
  backdrop-filter: blur(8px);
}

.area-card {
  background: white;
  border: 1px solid var(--border-color);
  border-radius: 10px;
  padding: clamp(1rem, 1.5vw, 1.25rem);
  margin-bottom: 1rem;
  transition: all 0.2s ease;
}

.area-card:hover {
  box-shadow: var(--shadow-md);
  transform: translateY(-2px);
  border-color: #cbd5e1;
}

.area-name-input {
  flex: 1;
  padding: 0.625rem;
  border: 1px solid var(--border-color);
  border-radius: 8px;
  font-size: clamp(0.875rem, 1.5vw, 1rem);
  transition: all 0.2s ease;
  color: var(--text-color);
}

.area-name-input:focus {
  border-color: var(--primary-color);
  outline: none;
  box-shadow: 0 0 0 2px rgba(99, 102, 241, 0.1);
}

.slider {
  width: 100%;
  height: 6px;
  -webkit-appearance: none;
  background: #f1f5f9;
  border-radius: 4px;
  outline: none;
  margin: 10px 0;
  background-image: linear-gradient(to right, var(--primary-color), var(--primary-color));
  background-size: 0% 100%;
  background-repeat: no-repeat;
}

.slider::-webkit-slider-thumb {
  -webkit-appearance: none;
  width: clamp(18px, 3vw, 22px);
  height: clamp(18px, 3vw, 22px);
  background: white;
  border: 2px solid var(--primary-color);
  border-radius: 50%;
  cursor: pointer;
  box-shadow: var(--shadow-sm);
  transition: all 0.2s ease;
}

.btn-primary, .btn-secondary {
  padding: clamp(0.625rem, 1vw, 0.875rem) clamp(1rem, 1.5vw, 1.5rem);
  border: none;
  border-radius: 8px;
  font-weight: 500;
  cursor: pointer;
  transition: all 0.15s ease;
  display: flex;
  align-items: center;
  gap: 0.625rem;
  font-size: clamp(0.875rem, 1.2vw, 1rem);
}

.btn-primary {
  background: var(--primary-color);
  color: white;
}

.btn-primary:hover {
  background: var(--primary-hover);
  transform: translateY(-1px);
}

.btn-secondary {
  background: var(--bg-subtle);
  color: var(--text-color);
  border: 1px solid var(--border-color);
}

.btn-secondary:hover {
  background: #f1f5f9;
  border-color: #cbd5e1;
  transform: translateY(-1px);
}

.btn-secondary:active {
  transform: translateY(0);
}

.btn-icon-remove {
  width: clamp(28px, 3vw, 32px);
  height: clamp(28px, 3vw, 32px);
  border: 1px solid var(--border-color);
  background: var(--bg-subtle);
  color: var(--secondary-color);
  border-radius: 50%;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: clamp(1.125rem, 1.5vw, 1.25rem);
  transition: all 0.2s ease;
}

.btn-icon-remove:hover {
  background: #fef2f2;
  color: var(--danger-color);
  border-color: #fecaca;
}

.wheel-display {
  background: white;
  border-radius: var(--border-radius);
  padding: clamp(1.5rem, 3vw, 2.5rem);
  box-shadow: var(--shadow-md);
  border: 1px solid var(--border-color);
}

.areas-container::-webkit-scrollbar {
  width: 5px;
}

.areas-container::-webkit-scrollbar-track {
  background: #f8fafc;
  border-radius: 3px;
}

.areas-container::-webkit-scrollbar-thumb {
  background: #cbd5e1;
  border-radius: 3px;
}

.areas-container::-webkit-scrollbar-thumb:hover {
  background: #94a3b8;
}

.value-label {
  color: var(--secondary-color);
  font-size: 0.875rem;
  font-weight: 500;
}

  </style>
