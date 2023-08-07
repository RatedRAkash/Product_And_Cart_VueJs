<template>

  <header class="top-bar spread">
    <nav class="top-bar-nav">
      <router-link to="/" class="top-bar-link">
        <i class="icofont-spoon-and-fork"></i>
        <span>Home</span>
      </router-link>
      <router-link to="/products" class="top-bar-link">
        <span>Products</span>
      </router-link>
      <router-link to="/past-orders" class="top-bar-link">
        <span>Past Orders</span>
      </router-link>
    </nav>

  <!-- Sidebar Right e SHOW koranor jonno ei code -->
    <a @click="toggleSideBarMethod" class="top-bar-cart-link">
      <i class="icofont-cart-alt icofont-1x"></i>
      <span>Cart ({{ totalQuantity }})</span>
    </a>

  </header>

  <router-view :inventory_var_from_parent="inventory" :addToCart="addToCart"/>

  <Sidebar
      v-if="showSideBar"
      v-bind:toggle_var="toggleSideBarMethod"
      v-bind:cart_var="cart"
      v-bind:inventory_var="inventory"
      v-bind:remove="removeItemFromCart"
  />

</template>

<script>

import food_data_from_server from './food.json'
import Sidebar from "@/components/Sidebar.vue";

export default {
  components: {
    Sidebar
  },

  data() {
    return {
      showSideBar: false,
      inventory: food_data_from_server,
      cart: {}
    }
  },

  // `computed` function Watches the Changes of the DATA_Variables
  computed: {
    // eikane arr Use kortase Nah ei Function
    totalQuantity() {
      const totalCartItems = Object.values(this.cart).reduce((sum, current) => {
        return sum + current
      }, 0)

      return totalCartItems
    },
  },

  methods: {
    addToCart(name, index, quantity) {
      if (!quantity) {
        quantity = 0
        console.log("Please Insert Value Greater Than 1")
        return
      }

      if (!this.cart[name]) {
        this.cart[name] = 0
      }
      this.cart[name] += quantity
      console.log(this.cart)
    },

    toggleSideBarMethod() {
      this.showSideBar = !this.showSideBar
    },

    removeItemFromCart(name) {
      delete this.cart[name]
    }
  },

  // lifecycle Hook Method... Component Virtual DOM er sathe attach howar agge ei `Mounted` variable Call dey
  // async mounted() {
  //   const res = await fetch('./food.json')
  //   const response_data = await res.json()
  //   this.inventory = response_data
  // },
}
</script>

<style scoped>
</style>
