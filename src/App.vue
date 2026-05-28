<script>
import ProductCard from './components/ProductCard.vue'
import Cart from './components/Cart.vue'

export default {
  name: 'App',

  components: {
    ProductCard,
    Cart
  },

  data() {
    return {
      selectedCategory: 'Все',

      newProductName: '',

      showCart: true,

      cart: [],

      products: [
        {
          id: 1,
          name: 'iPhone 17 pro',
          price: 110000,
          category: 'Телефоны',
          available: 1,
          image: 'iph.png'
        },
        {
          id: 2,
          name: 'Samsung Galaxy',
          price: 45000,
          category: 'Телефоны',
          available: 1,
        },
        {
          id: 3,
          name: 'MacBook Air',
          price: 120000,
          category: 'Ноутбуки',
          available: 0,
        },
        {
          id: 4,
          name: 'MacBook',
          price: 73000,
          category: 'Ноутбуки',
          available: 1,
        },
        {
          id: 5,
          name: 'AirPods 3 pro',
          price: 25000,
          category: 'Наушники',
          available: 0,
        }
      ]
    }
  },

  computed: {
    filteredProducts() {
      if (this.selectedCategory === 'Все') {
        return this.products
      }

      return this.products.filter(
        item => item.category === this.selectedCategory
      )
    },

    totalPrice() {
      return this.cart.reduce((sum, item) => {
        return sum + item.price
      }, 0)
    }
  },

  methods: {
    addToCart(product) {
      this.cart.push(product)
    },

    removeProduct(index) {
      this.products.splice(index, 1)
    },

    clearCart() {
      this.cart = []
    },

    toggleCart() {
      this.showCart = !this.showCart
    },

    addNewProduct() {
      if (this.newProductName.trim() === '') {
        return
      }

      const newItem = {
        id: Date.now(),
        name: this.newProductName,
        price: 50000,
        category: 'Телефоны',
        available: 1,
      }

      this.products.unshift(newItem)

      this.newProductName = ''
    }
  }
}
</script>

<template>
  <div>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css" rel="stylesheet">

    <div class="container py-4">

      <h1 class="custom-title text-center text-md-start mb-4">
        Интернет-магазин
      </h1>

      <div class="row mb-4">
        <div class="col-12 col-md-6">
          <input type="text" class="form-control" placeholder="Название товара" v-model="newProductName">
        </div>

        <div class="col-12 col-md-6 mt-2 mt-md-0">
          <select class="form-select"  v-model="selectedCategory">
            <option value="Все">Все категории</option>
            <option value="Телефоны">Телефоны</option>
            <option value="Ноутбуки">Ноутбуки</option>
            <option value="Наушники">Наушники</option>
          </select>
        </div>
      </div>

      <div class="mb-4">
        <button class="btn btn-success me-2" @click="addNewProduct">
          Добавить новый товар
        </button>

        <button class="btn btn-warning" @click="toggleCart">
          Показать / скрыть корзину
        </button>
      </div>

      <Cart v-if="showCart" :cart="cart" :totalPrice="totalPrice" @clear-cart="clearCart" class="mb-4"/>

      <div class="row">

        <div class="col-12 col-md-6 col-lg-4 mb-4" v-for="(item, index) in filteredProducts" :key="item.id">
          <ProductCard :product="item" :index="index" @add-to-cart="addToCart" @remove-product="removeProduct"/>
        </div>

      </div>

    </div>
  </div>
</template>