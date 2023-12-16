<script setup>
import { ref, inject, watch, computed } from 'vue'
import axios from 'axios'
import DrawerHead from './DrawerHead.vue'
import CartItemList from './CartItemList.vue'
import InfoBlock from './InfoBlock.vue'

const props = defineProps({
  totalPrice: Number,
  vatPrice: Number
})

const { cart, closeDrawer } = inject('cart')

const isCreating = ref(false)
const orderId = ref(null)

const createOrder = async () => {
  try {
    isCreating.value = true
    const { data } = await axios.post(`https://604781a0efa572c1.mokky.dev/orders`, {
      items: cart.value,
      totalPrice: props.totalPrice.value
    })

    cart.value = []

    orderId.value = data.id;
  } catch (err) {
    console.log(err)
  } finally {
    isCreating.value = false
  }
}

const cartIsEmpty = computed(() => cart.value.length === 0)
const buttonDisabled = computed(() => isCreating.value || cartIsEmpty.value)
</script>

<template>
  <div class="fixed z-10 top-0 h-full w-full bg-black opacity-70" />
  <div
    class="flex flex-col justify-between fixed h-full z-10 top-0 h-full right-0 w-96 bg-white px-10 py-7"
  >
    <DrawerHead />

    <div v-if="!totalPrice || orderId" class="flex h-full items-center">
      <InfoBlock
        v-if="!totalPrice && !orderId"
        title="Корзина пустая"
        description="Добавьте хотя бы одну пару кроссовок, чтобы сделать заказ."
        image-url="/package-icon.png"
      />
      <InfoBlock
        v-if="orderId"
        title="Заказ оформлен!"
        :description="`Ваш заказ №${orderId} скоро будет передан курьерской доставке`"
        image-url="/order-success-icon.png"
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
            @click="createOrder"
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
