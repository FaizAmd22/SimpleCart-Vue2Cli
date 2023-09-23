<!-- eslint-disable prettier/prettier -->
<template>
    <nav class="navbar navbar-light bg-light fixed-top d-flex justify-content-end align-items-end align-content-end">
        <div class="navbar-text ml-auto d-flex">
            <button class="me-3 btn btn-sm btn-outline-success" @click="$emit('toggle')">
                <font-awesome-icon icon="fa-solid fa-dollar-sign"></font-awesome-icon>
            </button>
            <div class="me-3" v-if="cart.length > 0">
                <button class="btn btn-success btn-sm" @click="$emit('checkoutToggle')">
                    <span class="badge rounded-pill text-bg-success">{{ cartQty }}</span>
                    <font-awesome-icon icon="fa-solid fa-cart-shopping mx-2" :style="{'margin-right': '10px'}"></font-awesome-icon>
                    <price-list :value="Number(cartTotal)"></price-list>
                </button>
                <!-- <div class="dropdown-menu dropdown-menu-end" aria-labelledby="dropdownCart">
                    <div v-for="(item, index) in cart" :key="index">
                        <div class="dropdown-item-text text-nowrap text-end">
                            <span class="badge rounded-pill text-bg-warning align-text-top">
                                {{ item.qty }}
                            </span>
                            {{ item.product.name }}
                            <b>{{ item.product.price * item.qty | currencyUSD  }}</b>
                            <a href="#" class="badge text-bg-danger text-white link-underline link-underline-opacity-0 rounded-pill ms-2 fw-bold" v-on:click.stop="$emit('delete', index)">-</a>
                        </div>
                    </div>
                </div> -->
            </div>
        </div>
    </nav>
</template>

<script>
import PriceList from "./PriceList.vue";
import { FontAwesomeIcon } from "@fortawesome/vue-fontawesome";

export default {
  name: "navigation-bar",
  filters: {
    currencyUSD: function (value) {
      return "$ " + Number.parseFloat(value).toFixed(2);
    },
  },
  components: {
    FontAwesomeIcon,
    PriceList,
  },
  props: ["cart", "cartQty", "cartTotal"],
};
</script>
