<template>
  <div class="modal-backdrop">
    <div class="modal-container">
      <header class="modal-header">
        <h2>{{ title }}</h2>
        <button class="close-btn" @click="$emit('close')">&times;</button>
      </header>
      <div class="modal-content">
        <FolderTree :folders="folders" @select="handleFolderSelect" />
      </div>
      <footer class="modal-footer">
        <button class="btn btn-cancel" @click="$emit('close')">Закрыть</button>
        <button
          class="btn btn-ok"
          :disabled="!selectedFolderId"
          @click="$emit('close')">
          Ок
        </button>
      </footer>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, defineProps } from 'vue';
import FolderTree from './FolderTree.vue';

defineProps({
  title: String,
  folders: Array,
});

const selectedFolderId = ref<number | null>(null);

function handleFolderSelect(folderId: number) {
  selectedFolderId.value = folderId;
}

</script>

<style scoped>
.modal-backdrop {
  position: fixed;
  inset: 0;
  background: rgba(0, 0, 0, 0.5);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 1000;
}

.modal-container {
  background: #183D3D;
  border-radius: 10px;
  box-shadow: 0 10px 20px rgba(0, 0, 0, 0.2);
  width: 400px;
  max-width: 90%;
  padding: 20px;
  display: flex;
  flex-direction: column;
  gap: 20px;
}

.modal-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.modal-header h2 {
  font-size: 18px;
  font-weight: bold;
  margin: 0;
  color: #5C8374;
}

.close-btn {
  background: none;
  border: none;
  font-size: 24px;
    color: #999;
  cursor: pointer;
  transition: color 0.3s ease;
}

.close-btn:hover {
  color: #333;
}

.modal-content {
  max-height: 300px;
  overflow-y: auto;
}

.modal-footer {
  display: flex;
  justify-content: flex-end;
  gap: 10px;
}

.btn {
  padding: 10px 20px;
  border: none;
  border-radius: 5px;
  font-size: 14px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.btn-cancel {
  background-color: #f5f5f5;
  color: #666;
}

.btn-cancel:hover {
  background-color: #851818;
}

.btn-ok {
  background-color: #4caf50;
  color: white;
}

.btn-ok:hover {
  background-color: #388e3c;
}

.btn-ok:disabled {
  background-color: #ccc;
  cursor: not-allowed;
}
</style>
