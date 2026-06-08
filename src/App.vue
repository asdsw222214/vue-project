<script setup>
import { ref } from 'vue';
import SiteHeader from './components/SiteHeader.vue';
import AddPriceForm from './components/AddPriceForm.vue';
import PriceRecordTable from './components/PriceRecordTable.vue';

// 集中管理資料狀態
const records = ref([
  { id: 1, date: '2026-05-13', name: 'RTX 5090', price: 71990 },
  { id: 2, date: '2026-05-13', name: 'RTX 5080', price: 35990 },
  { id: 3, date: '2026-05-12', name: 'RTX 4070 Ti Super', price: 28990 },
]);

// 新增紀錄處理
const handleAddRecord = (newRecord) => {
  records.value.unshift(newRecord);
};

// 刪除紀錄處理
const handleDeleteRecord = (id) => {
  records.value = records.value.filter(record => record.id !== id);
};
</script>

<template>
  <div class="app-dashboard">
    <SiteHeader />
    
    <main class="main-layout">
      <!-- 左側：新增表單 -->
      <aside class="sidebar">
        <AddPriceForm @onAddRecord="handleAddRecord" />
      </aside>

      <!-- 右側：資料表格 -->
      <section class="content">
        <PriceRecordTable 
          :records="records" 
          @onDelete="handleDeleteRecord" 
        />
      </section>
    </main>
  </div>
</template>

<style scoped>
.app-dashboard {
  max-width: 1200px;
  margin: 0 auto;
  padding: 40px 20px;
  min-height: 100vh;
  background-color: #f8fafc;
  font-family: 'PingFang TC', 'Microsoft JhengHei', sans-serif;
}

.main-layout {
  display: flex;
  gap: 30px;
  align-items: flex-start;
}

.sidebar {
  flex: 0 0 320px;
  position: sticky;
  top: 20px;
}

.content {
  flex: 1;
}

/* 響應式：手機版改為上下排列 */
@media (max-width: 850px) {
  .main-layout {
    flex-direction: column;
  }
  
  .sidebar {
    flex: none;
    width: 100%;
    position: static;
  }
}
</style>

<style>
/* 全域重置樣式 */
body {
  margin: 0;
  background-color: #f8fafc;
}
</style>


