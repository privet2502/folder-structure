<template>
  <ul class="folder-tree">
    <li v-for="folder in folders" :key="folder.id">
      <div
        class="folder-item"
        :class="{ selected: folder.id === selectedFolderId }"
        @click="toggleFolder(folder.id)">
        <span>{{ folder.name }}</span>
        <button v-if="folder.children && folder.children.length" class="toggle-btn">
          {{ expandedFolders.has(folder.id) ? '-' : '+' }}
        </button>
      </div>
      <FolderTree
        v-if="expandedFolders.has(folder.id)"
        :folders="folder.children"
        @select="$emit('select', $event)"
      />
    </li>
  </ul>
</template>

<script setup lang="ts">
import { defineEmits, defineProps, ref } from 'vue'

defineProps({
  folders: Array,
});

const expandedFolders = ref<Set<number>>(new Set());
const selectedFolderId = ref<number | null>(null);

const emit = defineEmits(['select']);

function toggleFolder(folderId: number) {
  if (expandedFolders.value.has(folderId)) {
    expandedFolders.value.delete(folderId);
  } else {
    expandedFolders.value.add(folderId);
  }

  selectedFolderId.value = folderId;
  emit('select', folderId);
}
</script>

<style scoped>
.folder-tree {
  list-style: none;
  padding: 0;
  margin: 0;
}

.folder-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 8px 12px;
  border: 1px solid #ddd;
  border-radius: 5px;
  margin-bottom: 5px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.folder-item:hover {
  background-color: #93B1A6;
}

.folder-item.selected {
  background-color: #4caf50;
  color: white;
}

.toggle-btn {
  background: none;
  border: none;
  font-size: 16px;
  cursor: pointer;
}
</style>
