<template>
  <div class="table-container">
    <div class="table-header">
      <h2>歷史價格紀錄</h2>
      <div class="search-bar">
        <input type="text" placeholder="搜尋商品..." v-model="searchQuery" />
        <i class="search-icon">🔍</i>
      </div>
    </div>
    
    <div class="table-wrapper">
      <table class="price-table">
        <thead>
          <tr>
            <th>日期</th>
            <th>商品名稱</th>
            <th>價格 (TWD)</th>
            <th>操作</th>
          </tr>
        </thead>
        <tbody>
          <PriceTableRow 
            v-for="record in filteredRecords" 
            :key="record.id" 
            :recordData="record"
            @onDelete="$emit('onDelete', record.id)" 
          />
          <tr v-if="filteredRecords.length === 0">
            <td colspan="4" class="no-data">目前沒有符合搜尋條件的紀錄</td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue';
import PriceTableRow from './PriceTableRow.vue';

const props = defineProps({
  records: {
    type: Array,
    required: true
  }
});

defineEmits(['onDelete']);

const searchQuery = ref('');

// 搜尋過濾邏輯
const filteredRecords = computed(() => {
  if (!searchQuery.value) return props.records;
  return props.records.filter(record => 
    record.name.toLowerCase().includes(searchQuery.value.toLowerCase())
  );
});
</script>

<style scoped>
.table-container {
  background: #fff;
  padding: 24px;
  border-radius: 12px;
  box-shadow: 0 4px 6px rgba(0,0,0,0.05);
  border: 1px solid #edf2f7;
}

.table-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 20px;
}

h2 {
  margin: 0;
  color: #2d3748;
  font-size: 1.5rem;
}

.search-bar {
  position: relative;
  width: 250px;
}

.search-bar input {
  width: 100%;
  padding: 10px 35px 10px 12px;
  border: 1px solid #e2e8f0;
  border-radius: 8px;
  font-size: 0.9rem;
  box-sizing: border-box;
}

.search-icon {
  position: absolute;
  right: 12px;
  top: 50%;
  transform: translateY(-50%);
  color: #a0aec0;
  font-style: normal;
}

.table-wrapper {
  overflow-x: auto;
}

.price-table {
  width: 100%;
  border-collapse: collapse;
}

.price-table th {
  text-align: left;
  padding: 12px 10px;
  color: #718096;
  font-size: 0.85rem;
  text-transform: uppercase;
  letter-spacing: 0.05em;
  border-bottom: 2px solid #edf2f7;
}

.no-data {
  text-align: center;
  padding: 40px;
  color: #a0aec0;
  font-style: italic;
}
</style>
