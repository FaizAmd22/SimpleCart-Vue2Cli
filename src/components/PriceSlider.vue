<!-- eslint-disable prettier/prettier -->
<template>
    <transition name="custom" enter-active-class="animate__animated animate__fadeInDown" leave-active-class="animate__animated animate__fadeOutUp">
            <div v-if="sliderStatus">
                <div class="align-items-center mt-3" v-bind:class="sliderState">
                    <label class="fw-bold mr-2" v-bind:class="label">Max $</label>
                    <input type="number" class="form-control mx-2"
                    style="width: 80px; text-align: center;" v-model="maxAmount" @change="$emit('update:maximum', maxAmount)">
                    <input type="range" class="form-range" min="0" max="200" v-model="maxAmount" @input="$emit('update:maximum', maxAmount)">
                </div>
            </div>
    </transition>
</template>

<script>
export default {
  name: "price-slider",
  data: function () {
    return {
      maxAmount: 50,
    };
  },
  props: ["sliderStatus", "maximum"],
  computed: {
    sliderState: function () {
      return this.sliderStatus ? "d-flex" : "d-none";
    },
  },
};
</script>

<style>
.fade-enter,
.fade-leave-to {
  opacity: 0;
}
.fade-enter-active,
.fade-leave-active {
  transition: all 0.5s ease-in;
}

.label {
  width: 100px;
  display: flex;
  justify-content: center;
  margin: auto;
}
</style>
