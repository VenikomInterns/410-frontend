<template>
  <main class="bg-dark custom-background-height">

    <div class="container pt-5">
      <div class="row pt-5">
        <div v-for="product in products" class="col-4 mb-4 text-center">

          <product-card :product="product"/>
          <h5 class="card bg-primary py-3">
            <button class="btn btn-dark w-50 mx-auto rounded-5" @click="remove(product.id)">Remove from favourites</button>
          </h5>
        </div>
      </div>
    </div>
  </main>
</template>

<script>
import ProductCard from "@/components/ProductCard";

export default {
  components: {ProductCard},
  data() {
    return {
      cartItems: [],
      products: [],
    }
  },
  methods: {
    remove(prodId) {
      const res = localStorage.getItem("cartItems");
      let favItems = [];
      if (res) {
        favItems = JSON.parse(res);
      }
      favItems = favItems.filter(id => id !== prodId)
      localStorage.setItem("cartItems", JSON.stringify(favItems));

      this.products = this.products.filter(product => product.id !== prodId);
    },
    async loadData() {
      try {
        this.loading = true;
        const products = await this.$axios.$get(
          "/api/allProducts"
        );
        this.products = products.data.filter(product => this.cartItems.includes(product.id));
      } catch (e) {
        console.log(e);
      } finally {
        this.loading = false;
      }
    },

  },
  mounted() {
    const res = localStorage.getItem("cartItems");
    let favItems = [];
    if (res) {
      favItems = JSON.parse(res);
    }
    this.cartItems = favItems;
    this.loadData();
  },
  name: "cart",
}
</script>
