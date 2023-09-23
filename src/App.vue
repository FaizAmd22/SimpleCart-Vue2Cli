<!-- eslint-disable prettier/prettier -->
<template>
  <div class="container" :style="{'margin-top': '8vh'}" id="app">
        <h1>IDShop</h1>
        <navigation-bar
            :cart="cart"
            :cartQty="cartQty"
            :cartTotal="cartTotal"
            @toggle="toggleSliderStatus"
            @checkoutToggle="toggleCheckoutStatus"
            @delete="deleteItem"
        ></navigation-bar>
        <price-slider
            :sliderStatus="sliderStatus"
            :maximum.sync="maximum"
        ></price-slider>
        <product-list
            :products="products"
            :maximum="maximum"
            @add="addItem"
        ></product-list>
        <checkout-menu
            :cart="cart"
            :cartTotal="cartTotal"
            :checkoutStatus="checkoutStatus"
            @add="addItem"
            @delete="deleteItem"
        ></checkout-menu>
  </div>
</template>

<script>
// import ProductMenu from './components/ProductMenu.vue';
import ProductList from "./components/ProductList.vue";
import PriceSlider from "./components/PriceSlider.vue";
import NavigationBar from "./components/NavigationBar.vue";
import CheckoutMenu from './components/CheckoutMenu.vue';

export default {
    name: "App",
    data: function () {
        return {
            maximum: 50,
            products: [],
            cart: [],
            sliderStatus: false,
            checkoutStatus: false,
        };
    },
    components: {
        // ProductMenu,
        PriceSlider,
        ProductList,
        NavigationBar,
        CheckoutMenu
    },
    mounted: function () {
        fetch("https://hplussport.com/api/products/order/price")
            .then((response) => response.json())
            .then((data) => {
            this.products = data;
        });
    },
    computed: {
        cartTotal: function () {
            let sum = 0;
            for (let key in this.cart) {
                sum = sum + this.cart[key].product.price * this.cart[key].qty;
            }
            return sum;
        },
        cartQty: function () {
            let qty = 0;
            for (let key in this.cart) {
                qty = qty + this.cart[key].qty;
            }
            return qty;
        },
    },
    methods: {
        toggleSliderStatus: function () {
            this.sliderStatus = !this.sliderStatus;
        },
        toggleCheckoutStatus: function () {
            this.checkoutStatus = !this.checkoutStatus;
        },
        addItem: function (product) {
            var productIndex;
            var productExist = this.cart.filter(function (item, index) {
                if (item.product.id == Number(product.id)) {
                    productIndex = index;
                    return true;
                }
                else {
                    return false;
                }
            });
            if (productExist.length) {
                this.cart[productIndex].qty++;
            }
            else {
                this.cart.push({ product: product, qty: 1 });
            }
        },
        deleteItem: function (key) {
            if (this.cart[key].qty > 1) {
                this.cart[key].qty--;
            }
            else {
                this.cart.splice(key, 1);
            }
        },
    },
};
</script>