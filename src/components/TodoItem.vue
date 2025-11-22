<script setup>
import { ref } from 'vue'

const props = defineProps({
  todo: {
    type: Object,
    required: true
  }
})

const emit = defineEmits(['delete-todo', 'update-todo'])

const isEditing = ref(false)
const tempText = ref('')

// 开始编辑
const startEdit = () => {
  isEditing.value = true
  tempText.value = props.todo.text 
}

// 保存编辑
const saveEdit = () => {
  if (tempText.value.trim() === '') {
    alert('内容不能为空')
    return
  }
  emit('update-todo', props.todo.id, tempText.value)
  isEditing.value = false
}

// 取消编辑
const cancelEdit = () => {
  isEditing.value = false
}

// 删除
const handleDelete = () => {
  emit('delete-todo', props.todo.id)
}
</script>

<template>
  <li class="todo-item">
    <div v-if="isEditing" class="edit-mode">
      <input type="text" v-model="tempText" @keyup.enter="saveEdit" class="edit-input">
      <div class="btn-group">
        <button @click="saveEdit" class="btn btn-save">保存</button>
        <button @click="cancelEdit" class="btn btn-cancel">取消</button>
      </div>
    </div>

    <div v-else class="view-mode">
      <span class="todo-text">{{ todo.text }}</span>
      <div class="btn-group">
        <button @click="startEdit" class="btn btn-edit">编辑</button>
        <button @click="handleDelete" class="btn btn-delete">删除</button>
      </div>
    </div>
  </li>
</template>

<style scoped>
.todo-item {
  background: white;
  padding: 15px 20px;
  margin-bottom: 15px;
  border-radius: 8px;
  box-shadow: 0 2px 5px rgba(0,0,0,0.05);
  list-style: none;
}

.view-mode, .edit-mode {
  display: flex;
  width: 100%;
  justify-content: space-between;
  align-items: center;
}

.todo-text {
  font-size: 18px;
  color: #444;
}

.edit-input {
  flex: 1;
  padding: 8px;
  margin-right: 10px;
  border: 1px solid #ccc;
  border-radius: 4px;
  font-size: 16px;
}

.btn-group {
  display: flex;
  gap: 8px;
}

.btn {
  border: none;
  padding: 8px 16px;
  border-radius: 6px;
  cursor: pointer;
  font-size: 14px;
  color: white;
}

.btn-delete { background-color: #dc3545; }
.btn-edit { background-color: #ffc107; color: #333; }
.btn-save { background-color: #28a745; }
.btn-cancel { background-color: #6c757d; }
</style>