# Vue 3 實作教學：顯示卡市場行情觀測站

## 1. 基本資訊區
- **姓名**：鄧皓文
- **班級**：資訊工程學系二年級
- **專案名稱**：顯示卡市場行情觀測站

---

## 2. 實作目標與執行流程

本專案旨在建立一個可以紀錄並追蹤顯示卡市場價格的儀表板。透過 Vue 3 的元件化開發，我們能更有效率地管理介面與資料。

### 第一步：環境建立 (Vite)
1. 使用 npm 建立 Vite 專案。
2. 進入資料夾並安裝所需依賴。
3. 啟動開發伺服器。

> [在此插入終端機執行畫面截圖]
> *預期畫面：看到終端機顯示伺服器已啟動，並提供一個 http://localhost:5173 的連結。*

### 第二步：元件開發
1. 依照設計稿拆解元件。
2. 於 `src/components` 目錄下建立 `.vue` 檔案。
3. 實作各元件的 HTML/CSS 與邏輯。

> [在此插入 VS Code 下 src/components 目錄結構截圖]
> *預期畫面：看到目錄下包含 SiteHeader, AddPriceForm, PriceRecordTable, PriceTableRow 等檔案。*

### 第三步：資料串接與測試
1. 在 `App.vue` 中管理全域狀態。
2. 測試新增資料與搜尋過濾功能是否正常。

> [在此插入網頁操作畫面截圖]
> *預期畫面：網頁上出現完整的儀表板，點擊「送出紀錄」後表格會即時更新。*

### 第四步：GitHub Actions 部署
1. 設定專案部署腳本（如 `deploy.sh` 或 GitHub Actions YAML）。
2. 將程式碼推送到 GitHub 觸發自動化建置與部署。

---

## 3. 元件架構分析（核心重點）

為了維持開發的高效率與代碼的可維護性，我們遵循**單一職責原則 (Single Responsibility Principle)** 將專案拆解為以下四個核心元件：

1. **`SiteHeader.vue` (標題元件)**
   - **功能**：負責顯示網站主標題與副標題。
   - **優點**：樣式獨立，未來若要更改標題風格只需修改此處。

2. **`AddPriceForm.vue` (表單元件)**
   - **功能**：提供資料輸入介面，包含日期、商品型號、爬取功能與價格輸入。
   - **解析**：專注於「資料獲取與校驗」，並將結果透過事件傳遞出去。

3. **`PriceRecordTable.vue` (表格容器)**
   - **功能**：負責表格的整體結構（thead/tbody）以及「搜尋過濾」邏輯。
   - **解析**：這是一個容器元件，內部會循環生成 `PriceTableRow`。

4. **`PriceTableRow.vue` (單行資料元件)**
   - **功能**：顯示單筆資料細節及提供刪除按鈕。
   - **重用性**：這是一個高度可重用的子元件，它可以被放在任何需要列出顯示卡資訊的地方。

---

## 4. 元件構成網頁的邏輯

### 匯入與排版 (`App.vue`)
在 Vue 3 的 `<script setup>` 中，我們可以直接匯入元件並在樣板中使用。`App.vue` 作為根元件，扮演著「指揮官」的角色：

```vue
<script setup>
import { ref } from 'vue';
import SiteHeader from './components/SiteHeader.vue';
import AddPriceForm from './components/AddPriceForm.vue';
import PriceRecordTable from './components/PriceRecordTable.vue';

// 狀態管理：存放所有的紀錄資料
const records = ref([
  { id: 1, date: '2026-05-13', name: 'RTX 5090', price: 71990 }
]);
</script>

<template>
  <div class="app-dashboard">
    <SiteHeader />
    <main class="main-layout">
      <AddPriceForm @onAddRecord="handleAddRecord" />
      <PriceRecordTable :records="records" @onDelete="handleDeleteRecord" />
    </main>
  </div>
</template>
```

### 資料流動邏輯 (Props & Emits)
這就是 Vue 的核心精神：**Props Down, Events Up**。

- **父到子 (Props)**：`App.vue` 將 `records` 陣列透過 `:records="records"` 傳給 `PriceRecordTable`，讓表格知道要顯示什麼。
- **子到父 (Emits)**：當使用者點擊 `PriceTableRow` 的刪除按鈕時，子元件會發出一個 `onDelete` 事件。父元件監聽到後，執行對應的刪除函數，資料更新後畫面會自動更新。

---

## 5. 技術亮點：為什麼要模組化？

使用 **單一檔案元件 (SFCs, Single File Components)** 進行開發有以下三大優勢：

1. **開發易讀性**：HTML、JS、CSS 都寫在同一個檔案內（但彼此區隔），工程師一眼就能看出這個元件在做什麼。
2. **樣式隔離 (Scoped CSS)**：透過 `<style scoped>`，我們不用擔心這個元件的 CSS 會影響到其他元件，解決了權重衝突的煩惱。
3. **維護與重構**：當「搜尋功能」壞掉時，我們知道只要去檢查 `PriceRecordTable.vue`，而不需要在數千行的程式碼中大海撈針。

---

**希望這份教學文件能幫助你順利踏入 Vue 3 的世界！只要理解了元件化的邏輯，你就能建立出各種複雜且優雅的網頁應用。**
