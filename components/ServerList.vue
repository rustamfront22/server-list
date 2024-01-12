<template>
  <ul class="overflow-auto h-[calc(100vh_-_80px)]">
    <li
        v-for="(server, key) in servers"
        :key="server.id"
        class="flex w-full px-4 py-2  text-gray-500 border-b focus:outline-none focus:ring-2 focus:ring-transparent hover:bg-gray-100 cursor-pointer"
        @click="$emit('selectServer', server)"
        :class="{'bg-gray-200': server.customer_id === currentServer?.customer_id}"
    >
      <p class="pr-4 text-lg font-bold text-gray-500">
        #{{ key + 1}}
      </p>
      <div class="text-left">
        <p class="text-xl font-bold line-clamp-1">{{ server.server_name }}</p>
        <span>{{ server_types[server.server_type] }}</span>
      </div>
      <button @click.prevent="$emit('deleteServer', server)" class="ml-auto pl-4 text-gray-400 focus:outline-none focus:ring-2 focus:ring-transparent hover:text-gray-500">
        <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24"><path fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 6h18m-2 0v14c0 1-1 2-2 2H7c-1 0-2-1-2-2V6m3 0V4c0-1 1-2 2-2h4c1 0 2 1 2 2v2"/></svg>
      </button>
    </li>
  </ul>
</template>

<script setup>
const props = defineProps(['servers', 'currentServer'])
const emits = defineEmits(['selectServer', 'deleteServer'])
const server_types = {
  vds: 'VDS',
  dedicated: 'Выделенный сервер',
  hosting: 'Хостинг'
}
</script>