<script setup>
import Card from '../components/Card.vue'

defineProps({
  items: Array
})

const onClickAdd = () => {
  alert('Добавить!')
}
</script>

<template>
  <div class="grid grid-cols-2 gap-10">
    <Card
      v-for="item in items"
      :key="item.id"
      :title="item.title"
      :imageUrl="item.imageUrl"
      :price="item.price"
      :is-favorite="true"
      :onClickAdd="onClickAdd"
    />
  </div>
</template>