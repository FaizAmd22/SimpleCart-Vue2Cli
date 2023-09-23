<!-- eslint-disable prettier/prettier -->
<template>
    <transition-group name="kostum" tag="div" enter-active-class="animate__animated animate__fadeInLeft" leave-active-class="animate__animated animate__fadeOutRight">
            <div class="row d-flex mb-3 align-items-center" v-for="(item, index) in showItem" :key="item.id" :data-index="index">
                    <div class="col-1 m-auto">
                        <button class="btn btn-info" @click="$emit('add', item)">+</button>
                    </div>
                    <div class="col-sm-4">
                        <img :src="item.image" :alt="item.name" class="img-fluid" >
                    </div>
                    <div class="col">
                        <h3 class="text-info">{{ item.name }}</h3>
                        <p class="mb-0">{{ item.description }}</p>
                        <div class="h5 float-right">
                            <price :value="item.price"></price>
                        </div>
                    </div>
            </div>
        </transition-group>
</template>

<script>
    import Price from "../components/PriceList.vue"

    export default {
        name: "product-list",
        components: {
            Price
        },
        props: ["products", "maximum"],
        computed: {
            showItem: function () {
                let max = this.maximum;
                return this.products.filter(function(item) {
                    return Math.trunc(item.price) <= max;
                })
            }
        }
    }
</script>
