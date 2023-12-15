<script setup>
import Card from '../components/Card.vue'

const onClickAdd = () => {
  alert('Добавить!')
}
</script>

<template>
  <div class="grid grid-cols-2 gap-10">
    <Card
      title="Мужские кроссовки Nike Blazer Mid Suede"
      imageUrl="/sneakers/sneakers-1.jpg"
      :price="5000"
      :is-favorite="true"
      :onClickAdd="onClickAdd"
    />
  </div>
</template>
