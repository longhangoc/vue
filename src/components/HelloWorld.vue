<template>
  <div class="life-wheel-container">
    <header class="wheel-header">
      <h1 class="text-gradient">Bánh Xe Cuộc Đời</h1>
      <p class="header-description">
        Tùy chỉnh các lĩnh vực và mức độ để xem bánh xe thể hiện cuộc sống của bạn.
      </p>
    </header>

    <div class="content">
      <!-- Controls Panel -->
      <section class="controls-panel">
        <div class="panel-header">
          <button @click="addArea" class="btn-secondary" :disabled="areas.length >= 12">
            <span class="btn-icon">+</span> Thêm lĩnh vực
          </button>
          <button @click="undo" class="btn-secondary" :disabled="undoStack.length === 0">
            <span class="btn-icon">↺</span> Undo
          </button>
          <button @click="redo" class="btn-secondary" :disabled="redoStack.length === 0">
            <span class="btn-icon">↻</span> Redo
          </button>
        </div>

        <!-- Wheel Mode Switch: Segmented Control -->
        <div class="wheel-mode-switch">
          <span class="mode-label">Chọn giao diện bánh xe:</span>
          <div class="mode-buttons">
            <button :class="{'mode-button': true, active: wheelMode==='classic'}"
                    @click="setWheelMode('classic')">Classic</button>
            <button :class="{'mode-button': true, active: wheelMode==='cute'}"
                    @click="setWheelMode('cute')">Kitty Cute</button>
          </div>
        </div>

        <div class="areas-container">
          <TransitionGroup name="list" tag="div" class="area-list">
            <div v-for="(area, i) in areas" :key="i" class="area-card">
              <div class="area-header">
                <div class="color-indicator" :style="{ backgroundColor: area.color }"></div>
                <input type="text"
                       class="area-name-input"
                       v-model="area.name"
                       @input="updateArea(i, 'name', $event.target.value)"
                       placeholder="Tên lĩnh vực" />
                <button class="btn-icon-remove"
                        @click="removeArea(i)"
                        :disabled="areas.length <= 3">
                  ×
                </button>
              </div>
              <div class="area-controls">
                <div class="value-control">
                  <span class="value-label">Mức độ: {{ area.value }}/10</span>
                  <!-- Dùng @change để hạn chế lưu trạng thái quá nhiều khi kéo slider -->
                  <input type="range"
                         class="slider"
                         min="0"
                         max="10"
                         v-model.number="area.value"
                         @change="updateArea(i, 'value', parseInt($event.target.value))" />
                </div>
                <input type="color"
                       class="color-picker"
                       v-model="area.color"
                       @input="updateArea(i, 'color', $event.target.value)"
                       title="Chọn màu" />
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
  name: 'HelloWorld',
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
      ],
      undoStack: [],
      redoStack: [],
      wheelMode: 'classic' // Các giá trị: 'classic', 'modern', 'minimal'
    }
  },
  methods: {
    cloneAreas() {
      return JSON.parse(JSON.stringify(this.areas));
    },
    pushState() {
      this.undoStack.push(this.cloneAreas());
      this.redoStack = [];
    },
    updateArea(index, property, value) {
      this.pushState();
      this.areas[index][property] = value;
      this.drawWheel();
      if (property === 'value') {
        this.$nextTick(() => {
          this.updateSliderBackground(document.querySelectorAll('.slider')[index]);
        });
      }
    },
    addArea() {
      if (this.areas.length >= 12) return;
      this.pushState();
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
        this.pushState();
        this.areas.splice(index, 1);
        this.drawWheel();
        this.$nextTick(() => {
          this.initializeSliders();
        });
      }
    },
    undo() {
      if (this.undoStack.length > 0) {
        this.redoStack.push(this.cloneAreas());
        this.areas = this.undoStack.pop();
        this.drawWheel();
      }
    },
    redo() {
      if (this.redoStack.length > 0) {
        this.undoStack.push(this.cloneAreas());
        this.areas = this.redoStack.pop();
        this.drawWheel();
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
    setWheelMode(mode) {
      this.wheelMode = mode;
      this.drawWheel();
    },
    drawWheel() {
      if (this.wheelMode === 'classic') {
        this.drawClassicWheel();
      } else if (this.wheelMode === 'cute') {
        this.drawCuteWheel();
      }
    },
    // --- Giao diện Classic ---
    drawClassicWheel() {
      const svg = this.$refs.wheelSvg;
      const centerX = 250, centerY = 250;
      const maxRadius = 200, outerRadius = maxRadius + 40;
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
        // Vẽ text path cho tên lĩnh vực
        const pathId = `textPath${i}`;
        const textRadius = maxRadius + 20;
        const isBottomHalf = midAngle > 0 && midAngle < Math.PI;
        let pathStart, pathEnd;
        if (isBottomHalf) {
          pathStart = { x: centerX + textRadius * Math.cos(endAngle), y: centerY + textRadius * Math.sin(endAngle) };
          pathEnd = { x: centerX + textRadius * Math.cos(startAngle), y: centerY + textRadius * Math.sin(startAngle) };
        } else {
          pathStart = { x: centerX + textRadius * Math.cos(startAngle), y: centerY + textRadius * Math.sin(startAngle) };
          pathEnd = { x: centerX + textRadius * Math.cos(endAngle), y: centerY + textRadius * Math.sin(endAngle) };
        }
        const path = document.createElementNS("http://www.w3.org/2000/svg", "path");
        path.setAttribute("id", pathId);
        path.setAttribute("d", `M ${pathStart.x} ${pathStart.y} A ${textRadius} ${textRadius} 0 ${isBottomHalf ? 0 : 1} ${pathEnd.x} ${pathEnd.y}`);
        path.setAttribute("fill", "none");
        defs.appendChild(path);
        const textEl = document.createElementNS("http://www.w3.org/2000/svg", "text");
        textEl.setAttribute("fill", "#fff");
        textEl.setAttribute("font-size", "12px");
        textEl.setAttribute("font-weight", "bold");
        const textPathElement = document.createElementNS("http://www.w3.org/1999/xlink", "textPath");
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
    // --- Giao diện Modern ---
    drawModernWheel() {
      const svg = this.$refs.wheelSvg;
      const centerX = 250, centerY = 250;
      const innerRadius = 100, outerRadius = 200;
      svg.innerHTML = '';
      const defs = document.createElementNS("http://www.w3.org/2000/svg", "defs");
      svg.appendChild(defs);
      // Thêm filter drop shadow
      const filter = document.createElementNS("http://www.w3.org/2000/svg", "filter");
      filter.setAttribute("id", "dropShadow");
      const feGaussianBlur = document.createElementNS("http://www.w3.org/2000/svg", "feGaussianBlur");
      feGaussianBlur.setAttribute("in", "SourceAlpha");
      feGaussianBlur.setAttribute("stdDeviation", "3");
      filter.appendChild(feGaussianBlur);
      const feOffset = document.createElementNS("http://www.w3.org/2000/svg", "feOffset");
      feOffset.setAttribute("dx", "2");
      feOffset.setAttribute("dy", "2");
      filter.appendChild(feOffset);
      const feMerge = document.createElementNS("http://www.w3.org/2000/svg", "feMerge");
      const feMergeNode1 = document.createElementNS("http://www.w3.org/2000/svg", "feMergeNode");
      const feMergeNode2 = document.createElementNS("http://www.w3.org/2000/svg", "feMergeNode");
      feMergeNode2.setAttribute("in", "SourceGraphic");
      feMerge.appendChild(feMergeNode1);
      feMerge.appendChild(feMergeNode2);
      filter.appendChild(feMerge);
      defs.appendChild(filter);
      const angleStep = (2 * Math.PI) / this.areas.length;
      this.areas.forEach((area, i) => {
        const startAngle = i * angleStep - Math.PI / 2;
        const endAngle = (i + 1) * angleStep - Math.PI / 2;
        const midAngle = (startAngle + endAngle) / 2;
        // Vẽ background donut segment
        const bgLargeArcFlag = (endAngle - startAngle) <= Math.PI ? 0 : 1;
        const x1 = centerX + innerRadius * Math.cos(startAngle);
        const y1 = centerY + innerRadius * Math.sin(startAngle);
        const x2 = centerX + outerRadius * Math.cos(startAngle);
        const y2 = centerY + outerRadius * Math.sin(startAngle);
        const x3 = centerX + outerRadius * Math.cos(endAngle);
        const y3 = centerY + outerRadius * Math.sin(endAngle);
        const x4 = centerX + innerRadius * Math.cos(endAngle);
        const y4 = centerY + innerRadius * Math.sin(endAngle);
        const bgD = `M ${x1} ${y1} L ${x2} ${y2} A ${outerRadius} ${outerRadius} 0 ${bgLargeArcFlag} 1 ${x3} ${y3} L ${x4} ${y4} A ${innerRadius} ${innerRadius} 0 ${bgLargeArcFlag} 0 ${x1} ${y1} Z`;
        const bgPath = document.createElementNS("http://www.w3.org/2000/svg", "path");
        bgPath.setAttribute("d", bgD);
        bgPath.setAttribute("fill", "#f9f9f9");
        svg.appendChild(bgPath);
        // Vẽ filled arc với drop shadow
        const filledRadius = innerRadius + (outerRadius - innerRadius) * (area.value / 10);
        const xFilled1 = centerX + innerRadius * Math.cos(startAngle);
        const yFilled1 = centerY + innerRadius * Math.sin(startAngle);
        const xFilled2 = centerX + filledRadius * Math.cos(startAngle);
        const yFilled2 = centerY + filledRadius * Math.sin(startAngle);
        const xFilled3 = centerX + filledRadius * Math.cos(endAngle);
        const yFilled3 = centerY + filledRadius * Math.sin(endAngle);
        const xFilled4 = centerX + innerRadius * Math.cos(endAngle);
        const yFilled4 = centerY + innerRadius * Math.sin(endAngle);
        const filledLargeArcFlag = (endAngle - startAngle) <= Math.PI ? 0 : 1;
        const filledD = `M ${xFilled1} ${yFilled1} L ${xFilled2} ${yFilled2} A ${filledRadius} ${filledRadius} 0 ${filledLargeArcFlag} 1 ${xFilled3} ${yFilled3} L ${xFilled4} ${yFilled4} A ${innerRadius} ${innerRadius} 0 ${filledLargeArcFlag} 0 ${xFilled1} ${yFilled1} Z`;
        const filledPath = document.createElementNS("http://www.w3.org/2000/svg", "path");
        filledPath.setAttribute("d", filledD);
        filledPath.setAttribute("fill", area.color);
        filledPath.setAttribute("fill-opacity", "0.85");
        filledPath.setAttribute("filter", "url(#dropShadow)");
        svg.appendChild(filledPath);
        // Text label
        const textRadius = innerRadius + (filledRadius - innerRadius) / 2;
        const textX = centerX + textRadius * Math.cos(midAngle);
        const textY = centerY + textRadius * Math.sin(midAngle);
        const textEl = document.createElementNS("http://www.w3.org/2000/svg", "text");
        textEl.setAttribute("x", textX);
        textEl.setAttribute("y", textY);
        textEl.setAttribute("fill", "#333");
        textEl.setAttribute("font-size", "12px");
        textEl.setAttribute("font-weight", "bold");
        textEl.setAttribute("text-anchor", "middle");
        textEl.setAttribute("dominant-baseline", "middle");
        textEl.textContent = area.name;
        svg.appendChild(textEl);
      });
    },
    // --- Giao diện dễ thương kiểu pastel cute ---
    drawCuteWheel() {
      const pastelColors = [
        '#ffecd2', '#a0d8ef', '#fdcbf1', '#ffe6fa', '#d1fdff', '#e2f0cb', '#f6dfeb', '#ffd6e0', '#e4c1f9', '#fff1e6', '#b5ead7', '#c7ceea'
      ];
      const cuteIcons = ['🐰','🐻','🦄','🐱','🐥','🍭','🥑','🌸','🎀','🍉','🧸','🦊'];
      const svg = this.$refs.wheelSvg;
      const centerX = 250, centerY = 250;
      const maxRadius = 200;
      svg.innerHTML = '';
      // Nền trắng sữa bo mềm
      const bg = document.createElementNS("http://www.w3.org/2000/svg", "circle");
      bg.setAttribute("cx", centerX);
      bg.setAttribute("cy", centerY);
      bg.setAttribute("r", maxRadius + 28);
      bg.setAttribute("fill", "#fffdfa");
      svg.appendChild(bg);
      // Vẽ vòng ngoài soft
      for (let i = 1; i <= 10; i++) {
        const circle = document.createElementNS("http://www.w3.org/2000/svg", "circle");
        circle.setAttribute("cx", centerX);
        circle.setAttribute("cy", centerY);
        circle.setAttribute("r", maxRadius * i / 10);
        circle.setAttribute("fill", "none");
        circle.setAttribute("stroke", '#f5e1ee');
        circle.setAttribute("stroke-width", "2.2");
        svg.appendChild(circle);
      }
      // Vẽ các sector pastel + cute icon/label
      const angleStep = (2 * Math.PI) / this.areas.length;
      this.areas.forEach((area, i) => {
        const pastel = pastelColors[i % pastelColors.length];
        const icon = cuteIcons[i % cuteIcons.length];
        const startAngle = i * angleStep - Math.PI/2;
        const endAngle = (i + 1) * angleStep - Math.PI/2;
        // Vùng pastel bo cung
        const x1 = centerX + maxRadius * Math.cos(startAngle);
        const y1 = centerY + maxRadius * Math.sin(startAngle);
        const x2 = centerX + maxRadius * Math.cos(endAngle);
        const y2 = centerY + maxRadius * Math.sin(endAngle);
        const path = document.createElementNS("http://www.w3.org/2000/svg", "path");
        const largeArc = (endAngle - startAngle) > Math.PI ? 1 : 0;
        const d = `M ${centerX} ${centerY} L ${x1} ${y1} A ${maxRadius} ${maxRadius} 0 ${largeArc} 1 ${x2} ${y2} Z`;
        path.setAttribute("d", d);
        path.setAttribute("fill", pastel);
        path.setAttribute("stroke", "#ffe2ff");
        path.setAttribute("stroke-width", "3.3");
        path.setAttribute("filter", "drop-shadow(0 0 6px #ffe6fa88)");
        svg.appendChild(path);
        // Vẽ sector value "kem" pastel nổi bật hơn
        const valueRadius = maxRadius * (area.value / 10);
        const x1v = centerX + valueRadius * Math.cos(startAngle);
        const y1v = centerY + valueRadius * Math.sin(startAngle);
        const x2v = centerX + valueRadius * Math.cos(endAngle);
        const y2v = centerY + valueRadius * Math.sin(endAngle);
        const pathV = document.createElementNS("http://www.w3.org/2000/svg", "path");
        const dV = `M ${centerX} ${centerY} L ${x1v} ${y1v} A ${valueRadius} ${valueRadius} 0 ${largeArc} 1 ${x2v} ${y2v} Z`;
        pathV.setAttribute("d", dV);
        pathV.setAttribute("fill", pastel);
        pathV.setAttribute("fill-opacity", "0.87");
        pathV.setAttribute("stroke", pastel);
        pathV.setAttribute("stroke-width", "1");
        svg.appendChild(pathV);
        // Hiện số lớn giữa sector
        const midAngle = (startAngle + endAngle) / 2;
        const textRadius = valueRadius * 0.55;
        const tx = centerX + textRadius * Math.cos(midAngle);
        const ty = centerY + textRadius * Math.sin(midAngle) + 2;
        const valueText = document.createElementNS("http://www.w3.org/2000/svg", "text");
        valueText.setAttribute("x", tx);
        valueText.setAttribute("y", ty);
        valueText.setAttribute("fill", pastel);
        valueText.setAttribute("font-size", "2em");
        valueText.setAttribute("font-weight", "bold");
        valueText.setAttribute("text-anchor", "middle");
        valueText.setAttribute("dominant-baseline", "middle");
        valueText.setAttribute("style", "font-family: 'Comic Sans MS', 'Baloo 2', 'Arial Rounded MT Bold', Arial, sans-serif;");
        valueText.textContent = area.value;
        svg.appendChild(valueText);
        // Hiện tên lĩnh vực giữa sector kèm icon đáng yêu
        const labelRadius = valueRadius * 1.15 < maxRadius * 0.81 ? maxRadius * 0.8 : valueRadius * 1.12;
        const lx = centerX + labelRadius * Math.cos(midAngle);
        const ly = centerY + labelRadius * Math.sin(midAngle) + 10;
        const labelText = document.createElementNS("http://www.w3.org/2000/svg", "text");
        labelText.setAttribute("x", lx);
        labelText.setAttribute("y", ly);
        labelText.setAttribute("fill", "#f47cc3");
        labelText.setAttribute("font-size", "1.06em");
        labelText.setAttribute("font-weight", "bold");
        labelText.setAttribute("text-anchor", "middle");
        labelText.setAttribute("dominant-baseline", "middle");
        labelText.setAttribute("style", "font-family: 'Comic Sans MS', 'Baloo 2', 'Arial Rounded MT Bold', Arial, sans-serif;");
        labelText.textContent = icon + ' ' + area.name;
        svg.appendChild(labelText);
      });
      // Đường phân cách sector pastel nhẹ
      for(let i = 0; i < this.areas.length; i++) {
        const angle = i * angleStep - Math.PI/2;
        const x = centerX + maxRadius * Math.cos(angle);
        const y = centerY + maxRadius * Math.sin(angle);
        const line = document.createElementNS("http://www.w3.org/2000/svg", "line");
        line.setAttribute("x1", centerX);
        line.setAttribute("y1", centerY);
        line.setAttribute("x2", x);
        line.setAttribute("y2", y);
        line.setAttribute("stroke", "#ffc4e6");
        line.setAttribute("stroke-width", "2");
        svg.appendChild(line);
      }
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
      const width = 500 * scaleFactor, height = 500 * scaleFactor;
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
  --font-base: 'Roboto', sans-serif;
  --border-radius: 12px;
  --shadow-sm: 0 2px 4px rgba(0, 0, 0, 0.08);
  --shadow-md: 0 4px 8px rgba(0, 0, 0, 0.1);
  --shadow-lg: 0 12px 24px rgba(0, 0, 0, 0.15);
  --transition: all 0.3s ease;
  --spacing-xs: 0.25rem;
  --spacing-sm: 0.5rem;
  --spacing-md: 1rem;
  --spacing-lg: 1.5rem;
}

/* Global Styles */
body {
  font-family: var(--font-base);
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

/* Header */
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
  margin-bottom: var(--spacing-sm);
}

.header-description {
  color: #666;
  font-size: clamp(1rem, 1.5vw, 1.2rem);
}

/* Layout */
.content {
  display: grid;
  grid-template-columns: minmax(300px, 1fr) minmax(300px, 2fr);
  gap: clamp(1rem, 2vw, 2rem);
  align-items: start;
}

/* Controls Panel */
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
  gap: var(--spacing-md);
}

/* Wheel Mode Switch: Segmented Control */
.wheel-mode-switch {
  display: flex;
  align-items: center;
  gap: var(--spacing-sm);
  margin-bottom: 1rem;
}

.mode-label {
  font-size: 0.9rem;
  color: var(--text-color);
  font-weight: 500;
}

.mode-buttons {
  display: flex;
  gap: 0.5rem;
}

.mode-button {
  padding: 0.5rem 1rem;
  border: 1px solid #ccc;
  background: #fff;
  border-radius: 999px;
  font-size: 0.9rem;
  letter-spacing: 0.5px;
  cursor: pointer;
  transition: background 0.3s ease, border 0.3s ease, color 0.3s ease, box-shadow 0.3s ease;
  color: #333; /* Màu chữ mặc định */
  outline: none;
}

.mode-button:focus {
  outline: none;
  box-shadow: 0 0 0 3px rgba(0, 123, 255, 0.3);
}

.mode-button:hover {
  background: #f0f0f0; /* Màu khi hover nhẹ nhàng */
  border-color: #bbb;
}

.mode-button.active {
  background: #007bff; /* Màu nền khi chọn */
  border-color: #0056b3;
  color: #fff; /* Đảm bảo chữ luôn hiển thị rõ ràng */
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.15);
}

/* Areas Container */
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

/* Area Card */
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
  gap: var(--spacing-sm);
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

/* Slider */
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

/* Color Picker */
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

/* Buttons */
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
  background: #e67e22;
  color: #fff;
}

.btn-primary:hover {
  background: #d35400;
}

.btn-secondary {
  background: #ecf0f1;
  color: #2c3e50;
  border: 1px solid #bdc3c7;
}

.btn-secondary:hover {
  background: #d0d7de;
}

.btn-icon-remove {
  width: clamp(24px, 3vw, 28px);
  height: clamp(24px, 3vw, 28px);
  border: none;
  background: var(--bg-light);
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

/* Action Buttons */
.action-buttons {
  display: flex;
  gap: clamp(0.5rem, 1vw, 1rem);
  margin-top: 1.5rem;
  justify-content: flex-end;
}

/* Wheel Display */
.wheel-display {
  background: #fff;
  border-radius: var(--border-radius);
  padding: 1.5rem;
  box-shadow: 0 8px 16px rgba(0, 0, 0, 0.1);
  position: relative;
  overflow: hidden;
}

.wheel-container {
  background: radial-gradient(circle at center, #fff, #f0f0f0);
  border-radius: 50%;
  padding: 1rem;
  position: relative;
}

.life-wheel {
  width: 100%;
  height: 100%;
  transition: transform 0.5s ease;
  filter: drop-shadow(0 4px 6px rgba(0, 0, 0, 0.1));
}

/* List Transition Animations */
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
    gap: var(--spacing-sm);
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
    margin-bottom: var(--spacing-sm);
  }
}
</style>