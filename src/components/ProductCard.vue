<script>
export default {
  name: 'ProductCard',

  props: {
    product: Object,
    index: Number
  },

  methods: {
    addToCart() {
      this.$emit('add-to-cart', this.product)
    },

    removeProduct() {
      this.$emit('remove-product', this.index)
    }
  }
}
</script>

<template>
  <div class="card h-100 shadow-sm">
    <img :src="product.image" class="card-img-top product-image" :alt="product.name">

    <div class="card-body d-flex flex-column">
      <h5 class="card-title">
        {{ product.name }}
      </h5>

      <p class="card-text">
        Категория: {{ product.category }}
      </p>

      <p class="card-text">
        Цена: {{ product.price }}
      </p>

      <p v-if="product.available" class="text-success">
        В наличии
      </p>

      <p v-else class="text-danger">
        Нет в наличии
      </p>

      <button class="btn btn-primary mt-auto" @click="addToCart">
        Добавить в корзину
      </button>

    </div>
  </div>
</template>
