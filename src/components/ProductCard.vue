<template>

  <div class="card">
    <div class="card-title">
      {{ single_product.name }}
    </div>
    <div class="card-body">
      <i class="icofont-10x icofont-{{ icofont-carrot.icon }}"></i>
      <form>
        <div class="row">
          <div class="cell">
            <label>Type:</label>
          </div>
          <div class="cell">
            <em>{{ single_product.type }}</em>
          </div>
        </div>
        <div class="row">
          <div class="cell">
            <label>Price:</label>
          </div>
          <div class="cell">
            ${{ single_product.price.USD }}
          </div>
        </div>
        <div class="row">
          <div class="cell">
            <label>Quantity:</label>
          </div>
          <div class="cell">
            <input type="number" v-model.number="quantity">
          </div>
        </div>
      </form>
    </div>
    <div class="card-footer">
      <button @click="addToCart(single_product.name, i, quantity)" class="btn btn-light">Add to cart</button>
    </div>
  </div>
</template>

<script>
export default {
  props: ['single_product', 'index', 'addToCart'],
  data (){
    return {
        quantity: 0
    }
  },
}
</script>