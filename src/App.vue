<script setup>
import TheHeader from './components/TheHeader.vue'
import CardList from './components/CardList.vue'
import Drawer from './components/Drawer.vue'
</script>

<template>
  <Drawer />

  <div class="bg-white w-full m-auto rounded-xl shadow-xl shadow-grey-200 mt-20">
    <TheHeader />

    <div class="p-10">
      <div class="flex justify-between">
        <h2 class="text-3xl font-bold mb-4">Все кроссовки</h2>
        <div class="flex items-center gap-4">
          <select
            class="py-2 px-3 border border-gray-200 focus:border-gray-400 rounded-md focus:outline-none"
          >
            <option value="name">По названию</option>
            <option value="price">По цене (дешевые)</option>
            <option value="price">По цене (дорогие)</option>
          </select>
          <div class="relative">
            <input
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

      <CardList />
    </div>
  </div>
</template>
