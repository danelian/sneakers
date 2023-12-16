<script setup>
import DrawerHead from './DrawerHead.vue'
import CartItemList from './CartItemList.vue';
import InfoBlock from './InfoBlock.vue'

const emit = defineEmits(['createOrder'])

defineProps({
  totalPrice: Number,
  vatPrice: Number,
  buttonDisabled: Boolean
})
</script>

<template>
  <div class="fixed z-10 top-0 h-full w-full bg-black opacity-70" />
  <div
    class="flex flex-col justify-between fixed h-full z-10 top-0 h-full right-0 w-96 bg-white px-10 py-7"
  >
    <DrawerHead />

    <div v-if="!totalPrice" class="flex h-full items-center">
      <InfoBlock 
        title="Корзина пустая" 
        description="Добавьте хотя бы одну пару кроссовок, чтобы сделать заказ."
        image-url="/package-icon.png"
      />
    </div>

    <div v-else>
      <CartItemList />
      
      <div class="flex flex-col flex-1 justify-between mt-auto">
        <div>
          <div class="flex flex-col gap-5">
            <div class="flex items-end gap-2">
              <span>Итого:</span>
              <div class="flex-1 border-b border-dashed" />
              <span class="font-bold">{{ totalPrice }} руб.</span>
            </div>

            <div class="flex items-end gap-2">
              <span>Налог 5%:</span>
              <div class="flex-1 border-b border-dashed" />
              <span class="font-bold">{{ vatPrice }} руб.</span>
            </div>
          </div>

          <button
            :disabled="buttonDisabled"
            @click="() => emit('createOrder')"
            class="flex justify-center items-center gap-3 w-full py-3 mt-10 bg-lime-500 text-white rounded-xl transition active:bg-lime-700 hover:bg-lime-600 disabled:cursor-auto disabled:!bg-gray-300"
          >
            Оформить заказ
            <img src="/arrow-next.svg" alt="Arrow" />
          </button>
        </div>
      </div>
    </div>
  </div>
</template>