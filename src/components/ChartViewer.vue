<script setup>
// 這裡可以預留圖表庫的載入邏輯
</script>

<template>
  <div class="chart-viewer">
    <div class="chart-header">
      <h3>趨勢分析圖表</h3>
    </div>
    <div class="chart-placeholder">
      <div class="bar bar-1"></div>
      <div class="bar bar-2"></div>
      <div class="bar bar-3"></div>
      <div class="bar bar-4"></div>
      <div class="bar bar-5"></div>
      <p>圖表區塊 (CSS 模擬元件)</p>
    </div>
  </div>
</template>

<style scoped>
.chart-viewer {
  background: #ffffff;
  border: 1px solid #e0e0e0;
  border-radius: 12px;
  padding: 1.5rem;
  margin-top: 20px;
}

.chart-header h3 {
  margin-top: 0;
  color: #2c3e50;
}

.chart-placeholder {
  height: 200px;
  background-color: #f9f9f9;
  border-radius: 8px;
  display: flex;
  align-items: flex-end;
  justify-content: space-around;
  padding: 20px;
  position: relative;
  border: 1px dashed #ccc;
}

.chart-placeholder p {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  color: #999;
  font-weight: bold;
}

.bar {
  width: 40px;
  background: linear-gradient(to top, #3498db, #2980b9);
  border-radius: 4px 4px 0 0;
}

.bar-1 { height: 40%; }
.bar-2 { height: 70%; }
.bar-3 { height: 55%; }
.bar-4 { height: 90%; }
.bar-5 { height: 65%; }
</style>
