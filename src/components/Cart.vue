<script>
export default {
  name: 'Cart',

  props: {
    cart: Array,
    totalPrice: Number
  }
}
</script>

<template>
  <div class="cart-box">
    <h3 class="mb-3">Корзина</h3>

    <p>Товаров: {{ cart.length }}</p>

    <ul class="list-group mb-3">
      <li class="list-group-item" v-for="(item, index) in cart" :key="index">
        {{ item.name }} - {{ item.price }} ₽
      </li>
    </ul>

    <h5>Общая сумма: {{ totalPrice }} ₽</h5>

    <button class="btn btn-danger mt-3" @click="$emit('clear-cart')">
      Очистить корзину
    </button>
  </div>
</template>

