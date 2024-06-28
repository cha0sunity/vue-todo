<template>
  <div class="dark:bg-gray-800 min-h-screen dark:text-white">
    <h1 class="text-3xl font-bold underline text-center py-5">Vue ToDo List</h1>
    <div class="flex justify-center py-2">
      <input
        @keyup.enter="handleClick"
        type="text"
        v-model="textBox"
        class="rounded p-2 dark:bg-gray-700 border-none focus:ring-2 focus:ring-blue-500"
      />
      <button
        @click="handleClick"
        class="ml-2 px-4 py-2 bg-blue-500 text-white rounded hover:bg-blue-600"
      >
        Add Item
      </button>
    </div>
    <div class="flex justify-center">
      <ul>
        <li v-for="(item, index) in list" :key="item" class="py-2">
          {{ item }}
          <button
            @click="deleteItem(index)"
            class="bg-red-500 hover:bg-red-600 text-white rounded ml-3 px-2"
          >
            X
          </button>
        </li>
      </ul>
    </div>
  </div>
</template>

<script setup>
import { onMounted, ref } from 'vue';
onMounted(() => {
  if (localStorage.getItem('list')) {
    list.value = JSON.parse(localStorage.getItem('list'));
  }
});

const textBox = ref('');
const list = ref([]);
const handleClick = () => {
  if (textBox.value === '') return;
  list.value.push(textBox.value);
  localStorage.setItem('list', JSON.stringify(list.value));
  textBox.value = '';
};
const deleteItem = (index) => {
  list.value.splice(index, 1);
  localStorage.setItem('list', JSON.stringify(list.value));
};
</script>
