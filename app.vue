<template>
  <div class="grid grid-cols-[1fr,2fr] gap-4 border h-[100vh]" v-if="db && db.length">
    <div class="border-r border-gray-300">
      <ServerHead @addServer="addServer" />
      <ServerList
          :servers="db"
          :currentServer="currentServer"
          @select-server="selectServer"
          @delete-server="db.splice(db.findIndex((item) => item.customer_id === $event.customer_id), 1)"
      />
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

db.value = db.value || []
const submit = (server) => {
  const index = db.value.findIndex((item) => item.customer_id === server.customer_id)
  db.value[index] = server
  currentServer.value = null
}
const selectServer = (value) => {
  currentServer.value = null

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

