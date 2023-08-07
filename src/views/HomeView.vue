<template>
  <div class="home">
    <h1>Home</h1>

    <div class="splash-container">
      <div class="splash">
        <h1>Splendid Food</h1>
      </div>
    </div>

    <main class="wrapper">

      <h2>Recommended</h2>

      <div class="recommended">

        <ProductCard v-for="(single_product, index) in inventory_var_from_parent.slice(0,3)"
                     :key="index"
                     class="card"
                     :index="index"
                     :single_product="single_product"
                     :addToCart="addToCart"
        />

      </div>

    </main>

  </div>
</template>

<script>
import ProductCard from '@/components/ProductCard.vue'

export default {
  name: 'HomeView',
  props: ['inventory_var_from_parent', 'addToCart'],

  components:{
    ProductCard
  },

  data (){
    return {

    }
  },
}
</script>
