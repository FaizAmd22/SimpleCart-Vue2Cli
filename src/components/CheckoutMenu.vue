<!-- eslint-disable prettier/prettier -->
<template>
  <transition name="fade">
    <div v-if="checkoutStatus">
      <div class="container fixed-bottom bg-dark bg-gradient rounded-top-4 p-4 flex-column overflow-auto h-50" v-bind:class="checkoutState">
        <h1 class="text-white">Checkout</h1>
        <table class="table table-hover table-dark table-striped">
          <caption class="text-end h3">
            <b>Total : </b>
            <price-list
              class="d-block text-white fw-light"
              :value="Number(cartTotal)"
            ></price-list>
          </caption>
          <thead>
            <tr>
              <th scope="col"></th>
              <th scope="col">Item</th>
              <th scope="col" class="text-center">Qty</th>
              <th scope="col" class="text-end">Price</th>
              <th scope="col" class="text-end">Sub-Total</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="(item, index) in cart" :key="item.product.id">
              <td class="text-center">
                <div class="btn-group">
                  <button @click="$emit('add', item.product)" class="btn btn-info">
                    +
                  </button>
                  <button
                    @click="$emit('delete', index)"
                    class="btn btn-outline-info"
                  >
                    -
                  </button>
                </div>
              </td>
              <th scope="row">{{ item.product.name }}</th>
              <th class="text-center">{{ item.qty }}</th>
              <th class="text-end">{{ Number(item.product.price) | currencyUSD }}</th>
              <th class="text-end">{{ Number(item.product.price * item.qty) | currencyUSD }}</th>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </transition>
</template>

<script>
import PriceList from "./PriceList.vue";

export default {
  name: "checkout-menu",
  props: ["cart", "cartTotal", "checkoutStatus"],
  components: {
    PriceList,
  },
  filters: {
    currencyUSD: function (value) {
      return "$ " + Number.parseFloat(value).toFixed(2);
    },
  },
  computed: {
    checkoutState: function() {
      return this.checkoutStatus ? "d-flex" : "d-none";
    }
  }
};
</script>
