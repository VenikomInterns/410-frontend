<template>
  <main class="bg-dark custom-background-height text-info">
    <div class="container py-5">
      <div class="py-5">
        <div>
            <h1>{{ product.name }}</h1>
            <h3>Price: {{product.price}} $</h3>
          <i class="fa  fa-2x" @click="addToFavourites()" :class="favClicked? 'fa-heart' : 'fa-heart-o'" aria-hidden="true"> ADD TO FAVOURITES CART</i>
          <h1>Product Images</h1>
        </div>
        <br>
        <div class="row">
          <div v-for="img in product.images" :key="img.id" class="col-12 col-lg-6" >
            <div class="ratio ratio-4x3">
              <img :src="img.url">
            </div>
          </div>
        </div>
      </div>
    </div>

  </main>
</template>

<script>
export default {
  created() {
    this.productId = this.$route.query.product;
  },
  data() {
    return {
      loading: false,
      productId: 0,
      product: {},
      quantity: 0,
      favClicked: false
    }
  },

  mounted() {
    if (this.productId !== 0) {
      this.loadData();
      const res = localStorage.getItem("cartItems");
      let favItems = [];
      if (res) {
        favItems = JSON.parse(res);
      }
      this.favClicked = favItems.includes(+this.productId);
    }
  },
  methods: {
    async loadData() {
      try {
        this.loading = true;
        const productResponse = await this.$axios.$get(
          "/api/products/" + this.productId
        );
        this.product = productResponse.data;
      } catch (e) {
        console.log(e);
      } finally {
        this.loading = false;
      }
    },
    addToFavourites(){
      this.favClicked=!this.favClicked;
      const res = localStorage.getItem("cartItems");
      let favItems = [];
      if (res) {
        favItems = JSON.parse(res);
      }
      const itemExists = favItems.includes(this.product.id)
      if (itemExists) {
        favItems = favItems.filter(id => id !== this.product.id)
      } else {
        favItems.push(this.product.id);
      }
      localStorage.setItem("cartItems", JSON.stringify(favItems));
    }
  },
  name: "product",
  props: {}
}
</script>
