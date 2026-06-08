<template>
  <tr class="data-row">
    <td>{{ recordData.date }}</td>
    <td>
      <span class="product-name">{{ recordData.name }}</span>
      <span class="detail-link">(點擊詳情)</span>
    </td>
    <td class="price-cell">NT$ {{ recordData.price.toLocaleString() }}</td>
    <td class="action-cell">
      <button class="delete-btn" @click="$emit('onDelete', recordData.id)" title="刪除紀錄">
        <i class="trash-icon">🗑️</i>
      </button>
    </td>
  </tr>
</template>

<script setup>
// 定義 Props，接收來自父元件的單筆資料
defineProps({
  recordData: {
    type: Object,
    required: true
  }
});

defineEmits(['onDelete']);
</script>

<style scoped>
.data-row {
  border-bottom: 1px solid #edf2f7;
  transition: background-color 0.2s;
}

.data-row:hover {
  background-color: #f7fafc;
}

.data-row td {
  padding: 14px 10px;
  color: #2d3748;
}

.product-name {
  font-weight: 500;
}

.detail-link {
  color: #a0aec0;
  font-size: 0.75rem;
  margin-left: 8px;
  cursor: pointer;
}

.detail-link:hover {
  color: #4a90e2;
  text-decoration: underline;
}

.price-cell {
  font-family: 'Courier New', Courier, monospace;
  font-weight: bold;
  color: #2c3e50;
}

.action-cell {
  text-align: center;
}

.delete-btn {
  background: none;
  border: none;
  cursor: pointer;
  font-size: 1.1rem;
  padding: 4px 8px;
  border-radius: 4px;
  transition: background 0.2s;
}

.delete-btn:hover {
  background-color: #fff5f5;
  color: #e53e3e;
}

.trash-icon {
  font-style: normal;
}
</style>
