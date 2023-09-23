<!-- eslint-disable prettier/prettier -->
<template>
    <div>
        <h1>IDShop</h1>
        <navigation-bar
            :cart="cart"
            :cartQty="cartQty"
            :cartTotal="cartTotal"
            @toggle-slide="toggleSlider"
            @delete-item="deleteItem"
        ></navigation-bar>
        <price-slider
            :sliderStatus="sliderStatus"
            :maximum="maximum"
        ></price-slider>
        <product-list
            :products="products"
            :maximum="maximum"
            @add-item="addItem"
        ></product-list>
    </div>
</template>

<script>
    import ProductList from "./ProductList.vue";
    import PriceSlider from "./PriceSlider.vue";
    import NavigationBar from "./NavigationBar.vue";

    export default {
        name: "products-menu",
        props: [
            "products",
            "maximum",
            "cart",
            "cartQty",
            "cartTotal",
            "sliderState",
            "sliderStatus"
        ],
        components: {
            PriceSlider,
            ProductList,
            NavigationBar,
        },
        methods: {
            toggleSlider: function() {
                this.$emit('toggle')
            },
            addItem: function(item) {
                this.$emit('add', item)
            },
            deleteItem: function(index) {
                this.$emit('delete', index)
            }
        }
    }
</script>