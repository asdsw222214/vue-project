<script setup>
import { reactive, computed } from 'vue';

const emit = defineEmits(['onAddRecord']);

const formData = reactive({
  date: new Date().toISOString().split('T')[0],
  name: '',
  price: null
});

const isFormValid = computed(() => {
  return formData.date && formData.name && formData.price > 0;
});

const handleSubmit = () => {
  if (!isFormValid.value) return;
  
  emit('onAddRecord', {
    id: Date.now(),
    date: formData.date,
    name: formData.name,
    price: Number(formData.price)
  });

  // 清空部分欄位
  formData.name = '';
  formData.price = null;
};
</script>

<template>
  <div class="add-price-form">
    <h3>新增價格紀錄</h3>
    <form @submit.prevent="handleSubmit">
      <div class="form-group">
        <label>日期</label>
        <input type="date" v-model="formData.date" required />
      </div>
      
      <div class="form-group">
        <label>商品型號</label>
        <div class="input-with-btn">
          <input type="text" v-model="formData.name" placeholder="例如: RTX 5090" required />
          <button type="button" class="crawl-btn">爬取</button>
        </div>
      </div>

      <div class="form-group">
        <label>目前價格 (TWD)</label>
        <input type="number" v-model="formData.price" placeholder="請輸入金額" required />
      </div>

      <button type="submit" class="submit-btn" :disabled="!isFormValid">
        送出紀錄
      </button>
    </form>
  </div>
</template>

<style scoped>
.add-price-form {
  background: #fff;
  padding: 24px;
  border-radius: 12px;
  box-shadow: 0 4px 6px rgba(0,0,0,0.05);
  border: 1px solid #edf2f7;
}

h3 {
  margin-top: 0;
  margin-bottom: 20px;
  color: #2d3748;
  font-size: 1.25rem;
}

.form-group {
  margin-bottom: 18px;
}

label {
  display: block;
  margin-bottom: 6px;
  font-weight: 600;
  color: #4a5568;
  font-size: 0.9rem;
}

input {
  width: 100%;
  padding: 10px;
  border: 1px solid #e2e8f0;
  border-radius: 6px;
  font-size: 1rem;
  box-sizing: border-box;
}

.input-with-btn {
  display: flex;
  gap: 8px;
}

.crawl-btn {
  padding: 0 16px;
  background-color: #f7fafc;
  border: 1px solid #e2e8f0;
  border-radius: 6px;
  cursor: pointer;
  color: #4a5568;
  white-space: nowrap;
}

.submit-btn {
  width: 100%;
  padding: 12px;
  background-color: #4299e1;
  color: white;
  border: none;
  border-radius: 6px;
  font-weight: bold;
  cursor: pointer;
  transition: background 0.2s;
}

.submit-btn:hover:not(:disabled) {
  background-color: #3182ce;
}

.submit-btn:disabled {
  background-color: #cbd5e0;
  cursor: not-allowed;
}
</style>
