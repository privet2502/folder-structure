<template>
  <div class="app">
    <button class="btn" @click="isModalOpen = true">Открыть</button>
    <FolderModal
      v-if="isModalOpen"
      :title="'Выбор папки'"
      :folders="folders"
      @close="isModalOpen = false"
      @select="handleSelect"
    />
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import FolderModal from './components/FolderModal.vue';

const isModalOpen = ref(false);
const folders = [
  { id: 1, name: 'Папка 1', children: [
      { id: 2, name: 'Папка 1.1', children: [] },
      { id: 3, name: 'Папка 1.2', children: [
          { id: 4, name: 'Папка 1.2.1', children: [] }
        ]}
    ]},
  { id: 5, name: 'Папка 2', children: [] },
];

function handleSelect(folderId: number) {
  console.log('Выбрана папка с ID:', folderId);
}
</script>

<style scoped>
.app {
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: #f4f4f9;
  border-radius: 10px;
}

.btn {
  background: linear-gradient(90deg, #4caf50, #81c784);
  border: none;
  border-radius: 8px;
  color: white;
  padding: 12px 24px;
  font-size: 16px;
  font-weight: bold;
  text-transform: uppercase;
  cursor: pointer;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  transition: all 0.3s ease;
}

.btn:hover {
  background: linear-gradient(90deg, #388e3c, #66bb6a);
  transform: translateY(-2px);
  box-shadow: 0 6px 8px rgba(0, 0, 0, 0.15);
}

.btn:active {
  transform: translateY(0);
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
}
</style>
