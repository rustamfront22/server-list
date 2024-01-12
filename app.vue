<template>
  <div class="grid md:grid-cols-[1fr,2fr] grid-cols-1 gap-4 border h-[100vh]" v-if="db && db.length">
    <div
        class="border-r border-gray-300 bg-white max-md:fixed transition-all z-10"
        :class="[{ 'left-0 w-full': serversActive}, {'left-[-380px] w-[380px]': !serversActive}]"
    >
      <ServerHead @addServer="addServer" />
      <ServerList
          :servers="db"
          :currentServer="currentServer"
          @select-server="selectServer"
          @delete-server="db.splice(db.findIndex((item) => item.customer_id === $event.customer_id), 1)"
      />
      <div
          class="md:hidden absolute top-4 w-12 h-12 flex items-center justify-center cursor-pointer text-gray-400 hover:text-gray-500 border rounded-lg border-gray-300 hover:border-gray-400 transition-all"
          @click="serversActive = !serversActive"
          :class="[{ 'right-2': serversActive}, {'-right-14': !serversActive}]"
      >
        <svg width="24" height="24" viewBox="0 0 24 24">
          <path fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M4.5 6.5h15M4.5 12h15m-15 5.5h15"/>
        </svg>
      </div>
    </div>
    <ServerForm
        v-if="currentServer"
        :currentServer="currentServer"
        @submit="submit"
    />
    <EmptySelect v-else />
  </div>
  <EmptyData
      v-else
      @addServer="addServer"
  />
</template>
<script setup>
import ServerHead from "~/components/ServerHead.vue";

const db = useCookie('db_servers')
const currentServer = ref(null)
const serversActive = ref(false)

db.value = db.value || []
const submit = (server) => {
  const index = db.value.findIndex((item) => item.customer_id === server.customer_id)
  db.value[index] = server
  currentServer.value = null
}
const selectServer = (value) => {
  currentServer.value = null
  serversActive.value = false
  nextTick(() => {
    currentServer.value = value
  })
}
const addServer = () => {
  db.value.push(
      {
        customer_id: 'user' + (db.value.length + 1),
        server_name: 'New server ' + (db.value.length + 1),
        server_type: 'vds'
      }
  )
  currentServer.value = db.value.at(-1)
}
</script>
<style scoped>
::-webkit-scrollbar {
  width: 5px;
  height: 5px;
}
::-webkit-scrollbar-track {
  background: #f1f1f1;
}
::-webkit-scrollbar-thumb {
  background: #888;
}
</style>

