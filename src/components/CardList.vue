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
    <Card imageUrl="/sneakers/sneakers-2.jpg" />
    <Card imageUrl="/sneakers/sneakers-3.jpg" />
    <Card imageUrl="/sneakers/sneakers-4.jpg" />
    <Card imageUrl="/sneakers/sneakers-5.jpg" />
  </div>
</template>
