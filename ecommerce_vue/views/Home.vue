<template>
  <div class="home">
    <section class="hero is-medium is-dark mb-6 slider-wrapper">
        <div class="hero-body has-text-centered slider-back">
            <p class="title mb-6">
                Welcome to E-Commerce
            </p>
            <p class="subtitle">biggest online store</p>
        </div>
    </section>

    <div class="columns is-multiline">
      <div class="column is-12">
        <h2 class="is-size-2 has-text-centered">Latest Products</h2>
      </div>
      <ProductBox v-for="product in latestProducts" v-bind:key="product.id" v-bind:product="product"/>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import ProductBox from "@/components/ProductBox.vue";
export default {
  name: 'Home',
  data() {
    return {
      latestProducts: []
    }
  },
  components: {
    ProductBox
  },
  mounted() {
    this.getLatestProducts()
    document.title = 'Home | E-commerce'
  },
  methods: {
    async getLatestProducts() {
      this.$store.commit('setIsLoading',true)
      await axios.get('/api/v1/latest-products/').then(response => {
        this.latestProducts = response.data
      }).catch(error => {
        console.log(error)
      })
      this.$store.commit('setIsLoading',false)
    }
  }
}
</script>
<style>
.slider-wrapper {
  border-radius: 6px;
}
.slider-back {
  border-radius: 6px;
  background: linear-gradient(to top, rgb(0 0 0 / 0.7), rgb(0 0 0 / 0)), url("../public/slider-background.jpg");
  background-size: cover;
}
</style>