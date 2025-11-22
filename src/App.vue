<!-- src/App.vue -->
<script setup>
import { ref } from 'vue'
import TodoInput from './components/TodoInput.vue'
import TodoItem from './components/TodoItem.vue'
import TodoFooter from './components/TodoFooter.vue'

const todos = ref([])

const handleAddTodo = (text) => {
  todos.value.push({ id: Date.now(), text: text })
}

const handleDeleteTodo = (id) => {
  todos.value = todos.value.filter(item => item.id !== id)
}

const handleUpdateTodo = (id, newText) => {
  const target = todos.value.find(item => item.id === id)
  if (target) target.text = newText
}

const handleClearAll = () => {
  todos.value = []
}
</script>

<template>
  <div class="container">
    <h1 class="title">本周待办事项</h1>

    <!-- 1. 列表和删除/编辑按钮 -->
    <ul class="list-container">
      <TodoItem 
        v-for="item in todos" 
        :key="item.id" 
        :todo="item" 
        @delete-todo="handleDeleteTodo"
        @update-todo="handleUpdateTodo"
      />
    </ul>

    <!-- 2. 输入框和添加按钮 -->
    <TodoInput @add-todo="handleAddTodo" />

    <!-- 3. 清空按钮 -->
    <TodoFooter v-if="todos.length > 0" @clear-all="handleClearAll" />
  </div>
</template>

<style scoped>
.container {
  max-width: 600px;
  margin: 50px auto;
  padding: 30px;
  background-color: #f5f7fa;
  border-radius: 10px;
  box-shadow: 0 4px 12px rgba(0,0,0,0.1);
  font-family: 'Microsoft YaHei', sans-serif;
}
.title {
  text-align: center;
  color: #333;
  margin-bottom: 30px;
  font-size: 28px;
  font-weight: bold;
}
.list-container {
  padding: 0;
  margin: 0 0 20px 0;
}
</style>