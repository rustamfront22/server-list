<template>
  <div class="flex items-center justify-between px-4 py-4 text-xl font-bold text-gray-500 border-b border-gray-300">
    <span class="block whitespace-nowrap pr-4">
      Список серверов
    </span>
    <button
        class="flex gap-2 items-center max-md:p-1 px-3 max-md:w-12 h-12 text-xl font-bold text-gray-500 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-gray-200 max-md:text-[0px] max-md:gap-0 max-md:mr-12 justify-center"
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