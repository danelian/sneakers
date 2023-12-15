<script setup>
import TheHeader from './components/TheHeader.vue'
import CardList from './components/CardList.vue'
</script>

<template>
  <div class="bg-white w-full m-auto rounded-xl shadow-xl shadow-grey-200 mt-20">
    <TheHeader />

    <div class="p-10">
      <h2 class="text-3xl font-bold mb-4">Все кроссовки</h2>

      <CardList />
    </div>
  </div>
</template>
