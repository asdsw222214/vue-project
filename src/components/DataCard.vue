<script setup>
defineProps({
  title: String,
  value: [String, Number],
  unit: String
})
</script>

<template>
  <div class="data-card">
    <div class="card-title">{{ title }}</div>
    <div class="card-value">
      <span class="value">{{ value }}</span>
      <span class="unit">{{ unit }}</span>
    </div>
  </div>
</template>

<style scoped>
.data-card {
  background: #ffffff;
  border: 1px solid #e0e0e0;
  border-radius: 12px;
  padding: 1.5rem;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.05);
  transition: transform 0.2s;
  flex: 1;
  min-width: 200px;
}

.data-card:hover {
  transform: translateY(-2px);
}

.card-title {
  color: #666;
  font-size: 0.9rem;
  margin-bottom: 0.5rem;
  font-weight: 600;
}

.card-value {
  display: flex;
  align-items: baseline;
}

.value {
  font-size: 1.8rem;
  font-weight: bold;
  color: #2c3e50;
  margin-right: 4px;
}

.unit {
  font-size: 0.9rem;
  color: #888;
}
</style>
