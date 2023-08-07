<template>

  <aside class="cart-container">
    <div class="cart">
      <h1 class="cart-title spread">
                    <span>
                      Cart
                      <i class="icofont-cart-alt icofont-1x"></i>
                    </span>
        <button @click="toggle_var" class="cart-close">&times;</button>
      </h1>

      <div class="cart-body">
        <table class="cart-table">
          <thead>
          <tr>
            <th><span class="sr-only">Product Image</span></th>
            <th>Product</th>
            <th>Price</th>
            <th>Qty</th>
            <th>Total</th>
            <th><span class="sr-only">Actions</span></th>
          </tr>
          </thead>
          <tbody>
          <tr v-for="(quantity, name, index) in cart_var" :key="index">
            <td><i class="icofont-carrot icofont-3x"></i></td>
            <td>{{ name }}</td>
            <td>${{ getPrice(name) }}</td>
            <td class="center">{{ quantity }}</td>
            <td>${{ quantity * getPrice(name) }}</td>
            <td class="center">
              <button @click="remove(name)" class="btn btn-light cart-remove">
                &times;
              </button>
            </td>
          </tr>
          </tbody>
        </table>

        <p class="center" v-if="!Object.keys(cart_var).length"><em>No items in cart</em></p>
        <div class="spread">
          <span><strong>Total:</strong> ${{ calculateTotal() }}</span>
          <button class="btn btn-light">Checkout</button>
        </div>
      </div>
    </div>
  </aside>

</template>

<script>
export default {
  props: ['toggle_var', 'cart_var', 'inventory_var', 'remove'],

  // `computed` function Watches the Changes of the variables in `Props` & will Update it
  computed: {
    // eikane arr Use kortase Nah ei Function
    cartTotal() {
      console.log("CartTotal:", this.cart_var.Raddishes)
      return (this.cart_var.Raddishes * 4.82).toFixed(2)
    },
  },

  methods: {
    // amader DATA te `name` Unique... So, amra `name` ke KEY hisave use korte parbo
    getPrice(name) {
      const var_product = this.inventory_var.find((product) => {
        return product.name === name
      })
      return var_product.price.USD
    },

    calculateTotal() {
      // const names = Object.keys(this.cart_var)
      // const total_sum = Object.values(this.cart_var).reduce((sum, current, index) => {
      //   return sum + (current * this.getPrice(names[index]))
      // })

      const total_sum = Object.entries(this.cart_var).reduce((sum, current, index) => {
        return sum + (current[1] * this.getPrice(current[0]))
      }, 0)

      return total_sum.toFixed(2)
    },
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
