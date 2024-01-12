<template>
  <div class="flex items-center justify-between px-4 py-4 text-xl font-bold text-gray-500 border-b border-gray-300">
    Список серверов
    <button
        class="flex gap-2 items-center px-4 py-2 text-xl font-bold text-gray-500 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-gray-200"
        @click="$emit('addServer')"
    >
      <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24"><path fill="none" stroke="currentColor" stroke-linecap="round" stroke-width="1.5" d="M12 17V7m-5 5h10"/></svg>
      Добавить
    </button>
  </div>
</template>
<script setup>
defineEmits(['addServer'])
</script>