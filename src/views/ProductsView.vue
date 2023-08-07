<template>
  <h1>Products</h1>

  <main class="wrapper">
    <div class="card-container">
      <ProductCard v-for="(single_product, index) in inventory_var_from_parent.slice(0,3)"
                   :key="index"
                   class="card"
                   :index="index"
                   :single_product="single_product"
                   :addToCart="addToCart"
      />
    </div>
  </main>

</template>

<script>
import ProductCard from '@/components/ProductCard.vue'

export default {
  name: 'ProductsView',
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