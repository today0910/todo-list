<script setup>
import { ref } from 'vue'

const emit = defineEmits(['add-todo'])

const inputValue = ref('')

const handleAdd = () => {
  if (inputValue.value.trim() === '') {
    alert('请输入待办事项内容！')
    return
  }
  emit('add-todo', inputValue.value)
  // 清空输入框
  inputValue.value = ''
}
</script>

<template>
  <div class="input-area">
    <input 
      type="text" 
      v-model="inputValue" 
      placeholder="请输入待办事项..." 
      class="main-input"
      @keyup.enter="handleAdd"
    >
    <button @click="handleAdd" class="btn btn-add">添加</button>
  </div>
</template>

<style scoped>
.input-area {
  display: flex;
  gap: 10px;
  margin-bottom: 20px;
}

.main-input {
  flex: 1;
  padding: 12px 15px;
  border: 2px solid #3b82f6;
  border-radius: 6px;
  font-size: 16px;
  outline: none;
}

.btn {
  border: none;
  padding: 8px 16px;
  border-radius: 6px;
  cursor: pointer;
  font-size: 14px;
  color: white;
}

.btn-add {
  background-color: #007bff;
  padding: 12px 25px;
  font-size: 16px;
}

.btn:hover {
  opacity: 0.9;
}
</style>