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
  --primary-color: #3498db;
  --secondary-color: #2ecc71;
  --danger-color: #e74c3c;
  --text-color: #2c3e50;
  --bg-light: #f8f9fa;
  --bg-medium: #e9ecef;
  --border-radius: 12px;
  --shadow-sm: 0 2px 4px rgba(0, 0, 0, 0.08);
  --shadow-md: 0 4px 8px rgba(0, 0, 0, 0.1);
  --shadow-lg: 0 12px 24px rgba(0, 0, 0, 0.15);
  --transition: all 0.3s ease;
}

body {
  font-family: 'Roboto', sans-serif;
  margin: 0;
  padding: 0;
  background-color: var(--bg-light);
  -webkit-font-smoothing: antialiased;
}

.life-wheel-container {
  max-width: 1200px;
  margin: 0 auto;
  padding: clamp(10px, 2vw, 20px);
  background: linear-gradient(135deg, var(--bg-light), var(--bg-medium));
  min-height: 100vh;
}

.wheel-header {
  text-align: center;
  margin-bottom: clamp(1rem, 3vw, 2rem);
  padding: clamp(1rem, 3vw, 2rem) 0;
}

.text-gradient {
  font-size: clamp(2rem, 4vw, 3rem);
  background: linear-gradient(45deg, var(--primary-color), var(--secondary-color));
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  margin-bottom: 0.5rem;
}

.header-description {
  color: #666;
  font-size: clamp(1rem, 1.5vw, 1.2rem);
}

.content {
  display: grid;
  grid-template-columns: minmax(300px, 1fr) minmax(300px, 2fr);
  gap: clamp(1rem, 2vw, 2rem);
  align-items: start;
}

.controls-panel {
  background: #fff;
  border-radius: var(--border-radius);
  padding: clamp(1rem, 2vw, 1.5rem);
  box-shadow: var(--shadow-md);
  height: fit-content;
}

.panel-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: clamp(1rem, 2vw, 1.5rem);
  flex-wrap: wrap;
  gap: 1rem;
}

.panel-header h2 {
  font-size: clamp(1.25rem, 2vw, 1.5rem);
  color: var(--text-color);
  margin: 0;
}

.areas-container {
  max-height: clamp(40vh, 50vh, 60vh);
  overflow-y: auto;
  padding-right: 0.5rem;
  scrollbar-width: thin;
  scrollbar-color: var(--primary-color) #f1f1f1;
}

.areas-container::-webkit-scrollbar {
  width: 6px;
}

.areas-container::-webkit-scrollbar-track {
  background: #f1f1f1;
  border-radius: 3px;
}

.areas-container::-webkit-scrollbar-thumb {
  background: var(--primary-color);
  border-radius: 3px;
}

.area-card {
  background: #fff;
  border: 1px solid #e1e4e8;
  border-radius: 8px;
  padding: clamp(0.75rem, 1.5vw, 1rem);
  margin-bottom: 1rem;
  transition: var(--transition);
}

.area-card:hover {
  box-shadow: var(--shadow-sm);
  transform: translateY(-2px);
}

.area-header {
  display: flex;
  align-items: center;
  gap: 0.75rem;
  margin-bottom: 1rem;
}

.color-indicator {
  width: clamp(24px, 4vw, 30px);
  height: clamp(24px, 4vw, 30px);
  border-radius: 50%;
  border: 2px solid #fff;
  box-shadow: var(--shadow-sm);
  flex-shrink: 0;
}

.area-name-input {
  flex: 1;
  padding: 0.5rem;
  border: 1px solid #e1e4e8;
  border-radius: 6px;
  font-size: clamp(0.875rem, 1.5vw, 1rem);
  transition: border-color 0.3s ease;
  min-width: 0;
}

.area-name-input:focus {
  border-color: var(--primary-color);
  outline: none;
  box-shadow: 0 0 0 2px rgba(52, 152, 219, 0.2);
}

.area-controls {
  display: flex;
  align-items: center;
  gap: clamp(0.5rem, 1vw, 1rem);
}

.value-control {
  flex: 1;
  min-width: 0;
}

.value-label {
  display: block;
  font-size: clamp(0.75rem, 1.2vw, 0.9rem);
  color: #4a5568;
  margin-bottom: 0.5rem;
  font-weight: 500;
}

.slider {
  width: 100%;
  height: 8px;
  -webkit-appearance: none;
  appearance: none;
  background: #e1e4e8;
  border-radius: 4px;
  outline: none;
  margin: 10px 0;
  background-image: linear-gradient(to right, var(--primary-color), var(--primary-color));
  background-size: 0% 100%;
  background-repeat: no-repeat;
  cursor: pointer;
  transition: background-size 0.3s ease;
}

.slider::-webkit-slider-thumb {
  -webkit-appearance: none;
  appearance: none;
  width: clamp(20px, 3vw, 24px);
  height: clamp(20px, 3vw, 24px);
  background: #fff;
  border: 2px solid var(--primary-color);
  border-radius: 50%;
  cursor: pointer;
  box-shadow: var(--shadow-sm);
  transition: transform 0.2s ease;
}

.slider::-webkit-slider-thumb:hover {
  transform: scale(1.1);
}

.slider::-moz-range-thumb {
  width: clamp(20px, 3vw, 24px);
  height: clamp(20px, 3vw, 24px);
  background: #fff;
  border: 2px solid var(--primary-color);
  border-radius: 50%;
  cursor: pointer;
  box-shadow: var(--shadow-sm);
  transition: transform 0.2s ease;
}

.slider::-moz-range-thumb:hover {
  transform: scale(1.1);
}

.color-picker {
  width: clamp(32px, 5vw, 40px);
  height: clamp(32px, 5vw, 40px);
  border: none;
  border-radius: 8px;
  cursor: pointer;
  padding: 2px;
  flex-shrink: 0;
  box-shadow: var(--shadow-sm);
}

.btn-primary,
.btn-secondary {
  padding: clamp(0.5rem, 1vw, 0.75rem) clamp(0.75rem, 1.5vw, 1.25rem);
  border: none;
  border-radius: 6px;
  font-weight: 500;
  cursor: pointer;
  transition: var(--transition);
  display: flex;
  align-items: center;
  gap: 0.5rem;
  font-size: clamp(0.875rem, 1.2vw, 1rem);
  white-space: nowrap;
}

.btn-primary {
  background: var(--primary-color);
  color: #fff;
}

.btn-primary:hover {
  background: #2980b9;
}

.btn-secondary {
  background: #f8f9fa;
  color: var(--text-color);
  border: 1px solid #e1e4e8;
}

.btn-secondary:hover {
  background: #e9ecef;
}

.btn-icon-remove {
  width: clamp(24px, 3vw, 28px);
  height: clamp(24px, 3vw, 28px);
  border: none;
  background: #f8f9fa;
  color: #666;
  border-radius: 50%;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: clamp(1rem, 1.5vw, 1.25rem);
  transition: var(--transition);
  flex-shrink: 0;
}

.btn-icon-remove:hover {
  background: var(--danger-color);
  color: #fff;
}

.action-buttons {
  display: flex;
  gap: clamp(0.5rem, 1vw, 1rem);
  margin-top: 1.5rem;
  justify-content: flex-end;
}

.wheel-display {
  background: #fff;
  border-radius: var(--border-radius);
  padding: clamp(1rem, 3vw, 2rem);
  box-shadow: var(--shadow-md);
}

.wheel-container {
  max-width: 100%;
  aspect-ratio: 1;
}

.life-wheel {
  width: 100%;
  height: 100%;
}

/* Animations */
.list-enter-active,
.list-leave-active {
  transition: opacity 0.5s, transform 0.5s;
}

.list-enter-from,
.list-leave-to {
  opacity: 0;
  transform: translateX(-30px);
}

/* Responsive Breakpoints */
@media (max-width: 1200px) {
  .life-wheel-container {
    max-width: 100%;
  }
}

@media (max-width: 1024px) {
  .content {
    grid-template-columns: 1fr;
    gap: 1.5rem;
  }
  
  .wheel-display {
    order: -1;
    max-width: 600px;
    margin: 0 auto;
  }

  .controls-panel {
    max-width: 600px;
    margin: 0 auto;
  }
}

@media (max-width: 768px) {
  .panel-header {
    flex-direction: column;
    align-items: stretch;
  }

  .action-buttons {
    flex-direction: column;
  }

  .btn-primary,
  .btn-secondary {
    width: 100%;
    justify-content: center;
  }

  .areas-container {
    max-height: 50vh;
  }
}

@media (max-width: 480px) {
  .area-controls {
    flex-direction: column;
    gap: 0.75rem;
  }

  .color-picker {
    width: 100%;
    height: 32px;
  }

  .area-header {
    flex-wrap: wrap;
  }

  .area-name-input {
    width: 100%;
    order: -1;
    margin-bottom: 0.5rem;
  }
}
  </style>
  
