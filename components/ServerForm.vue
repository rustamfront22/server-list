<template>
  <form class="flex flex-col items-center justify-center h-full lg:p-20 p-5">
    <blockquote class="font-bold text-gray-500 mb-6">
      <h2 class="text-2xl mb-6">Редактирование сервера</h2>
      <p class="text-gray-400">
        Ниже представлены данные выбранного сервера. Вы можете изменить их и
        нажать кнопку "Сохранить", чтобы сохранить изменения
      </p>
    </blockquote>
    <div class="flex flex-col w-full">
      <label class="text-md font-bold text-gray-500 mb-2"
        >Название сервера</label
      >
      <input
        id="server_name"
        class="w-full px-4 py-2 mb-4 text-lg text-gray-500 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-gray-200"
        v-model="state.server_name"
      />
    </div>
    <div class="flex flex-col w-full">
      <label class="text-md font-bold text-gray-500 mb-2">Тип сервера</label>
      <select
        class="w-full px-4 py-2 mb-4 text-lg text-gray-500 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-gray-200 appearance-none bg-[url('/images/arrow-down.svg')] bg-no-repeat bg-[calc(100%_-_10px)_center] bg-white"
        v-model="state.server_type"
      >
        <option value="vds">VDS</option>
        <option value="dedicated">Выделенный сервер</option>
        <option value="hosting">Хостинг</option>
      </select>
    </div>
    <button
      class="w-full px-4 py-2 mb-4 text-xl font-bold text-gray-500 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-gray-200 mt-4"
      @click.prevent="submit"
    >
      Сохранить
    </button>
  </form>
</template>
<script setup>
const props = defineProps(["currentServer"]);
const emits = defineEmits(["submit"]);
const state = reactive({
  customer_id: "",
  server_name: "",
  server_type: "",
});
onMounted(() => {
  state.customer_id = props.currentServer.customer_id;
  state.server_name = props.currentServer.server_name;
  state.server_type = props.currentServer.server_type;
  document.querySelector("#server_name").focus();
});
const submit = () => {
  if (!state.server_name) {
    return;
  }
  emits("submit", state);
};
</script>