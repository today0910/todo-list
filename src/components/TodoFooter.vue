<script setup>
const emit = defineEmits(['clear-all'])

const handleClear = () => {
  if (confirm('确定要清空所有事项吗？')) {
    emit('clear-all')
  }
}
</script>

<template>
  <div class="footer">
    <button @click="handleClear" class="btn btn-clear">清空所有</button>
  </div>
</template>

<style scoped>
.footer {
  text-align: center;
  margin-top: 20px;
}

.btn-clear {
  border: none;
  border-radius: 6px;
  cursor: pointer;
  color: white;
  background-color: #6c757d;
  padding: 10px 30px;
  font-size: 16px;
}
</style>