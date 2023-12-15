<script setup>
import { onMounted, reactive, ref, watch } from 'vue'
import axios from 'axios';

import TheHeader from './components/TheHeader.vue'
import CardList from './components/CardList.vue'
import Drawer from './components/Drawer.vue'

const items = ref([])

const filters = reactive({
  sortBy: 'title',
  searchQuery: ''
});

const onChangeSelect = (event) => {
  filters.sortBy = event.target.value
}

const onChangeSearchInput = (event) => {
  filters.searchQuery = event.target.value
}

const fetchItems = async () => {
  try {
    const params = {
      sortBy: filters.sortBy
    }

    if (filters.searchQuery) {
      params.title = `*${filters.searchQuery}*`
    }

    const { data } = await axios.get(
      `https://604781a0efa572c1.mokky.dev/items`, {
        params
      })
    items.value = data;
  } catch (err) {
    console.log(err)
  }
}

onMounted(fetchItems)
watch(filters, fetchItems)
</script>

<template>
  <!-- <Drawer /> -->

  <div class="bg-white w-full m-auto rounded-xl shadow-xl shadow-grey-200 mt-20">
    <TheHeader />

    <div class="p-10">
      <div class="flex justify-between">
        <h2 class="text-3xl font-bold mb-4">Все кроссовки</h2>
        <div class="flex items-center gap-4">
          <select 
            @change="onChangeSelect"
            class="py-2 px-3 border border-gray-200 focus:border-gray-400 rounded-md focus:outline-none"
          >
            <option value="name">По названию</option>
            <option value="price">По цене (дешевые)</option>
            <option value="-price">По цене (дорогие)</option>
          </select>
          <div class="relative">
            <input
              @input="onChangeSearchInput"
              type="text"
              class="border border-gray-200 rounded-md py-2 pl-10 pr-4 focus:outline-none focus:border-gray-400"
              placeholder="Поиск..."
            />
            <div class="absolute inset-y-0 left-0 pl-3 flex items-center pointer-events-none">
              <img src="/search.svg" />
            </div>
          </div>
        </div>
      </div>

      <CardList :items="items" />
    </div>
  </div>
</template>
