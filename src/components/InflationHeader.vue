<script setup>
defineProps({
  title: {
    type: String,
    default: '通貨膨脹分析儀表板'
  }
})
</script>

<template>
  <header class="inflation-header">
    <h1>{{ title }}</h1>
  </header>
</template>

<style scoped>
.inflation-header {
  background-color: #2c3e50;
  color: white;
  padding: 1rem 2rem;
  text-align: center;
  border-radius: 8px;
  margin-bottom: 20px;
}
h1 {
  margin: 0;
  font-size: 1.8rem;
}
</style>
