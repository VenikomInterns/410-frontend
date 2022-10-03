<template>
  <main class="bg-dark  custom-background-height">
    <div class="container text-center py-5">
      <h1 class="py-5 text-info fw-bolder">Choose a Category:</h1>
      <div class="row gy-3 gx-3 pb-5">
        <div class="col-12 col-md-4 col-lg-2 text-center" @click="changeSelected(-1)">
          <div class="card bg-secondary rounded-5 fw-bolder">All categories</div>
        </div>
        <div v-for="category in categories" class="col-12 col-md-4 col-lg-2 text-center"><!--Missing :key="" attriubte-->
          <div class="card bg-secondary rounded-5 fw-bolder" @click="changeSelected(category.id)">{{ category.name }}</div>
        </div>
      </div>


      <div class="row gy-4 gx-4 px-5 py-3">
        <div class="col-12 col-md-6 col-lg-4" v-for="product in products" 
             v-if="product.category_id === selected || selected===-1" :key="product.id"> <!--you can'y use v-for and v-if in same tag-->
          <product-card :product="product"/>
        </div>
      </div>
    </div>

    <nav aria-label="Page navigation example ">
      <ul class="pagination justify-content-center mb-0 pb-5">
        <li class="page-item">
          <button :disabled="currentPage === 1" class="page-link" @click="loadProducts(currentPage - 1)">Previous</button>
        </li>
        <li class="page-item" v-for="i in (totalPages)">
          <button class="page-link" :class="i === currentPage ? 'bg-secondary': ''" @click="loadProducts(i)">{{i}}</button>
        </li>
        <li class="page-item">
          <button :disabled="currentPage === totalPages" class="page-link" @click="loadProducts(currentPage + 1)">Next</button>
        </li>
      </ul>
    </nav>

  </main>
</template>

<script>
import ProductCard from "~/components/ProductCard";

export default {
  name: 'products',
  components: {ProductCard},
  async mounted() {
    await this.loadData();
  },
  data() {
    return {
      loading: false,
      categories: [],
      products: [],
      selected: -1,
      currentPage: 1,
      totalPages: 1,
    };
  },
  methods: {
    async loadData() {
      try {
        this.loading = true;
        const dataCategories = await this.$axios.$get(
          "/api/categories"
        );
        dataCategories.data.forEach((element) => {
          this.categories.push(element);
        });
        this.loadProducts(1);
      } catch (e) {
        console.log(e);
      } finally {
        this.loading = false;
      }
    },
    async loadProducts(page) {
      try {
        this.loading = true;
        let dataProducts = await this.$axios.$get(
          `/api/products/?page=${page}`
        );
        if(this.selected===-1){
          dataProducts = await this.$axios.$get(
            `/api/products/?page=${page}`
          );
        }else {
          dataProducts = await this.$axios.$get(
            `/api/productsOfCategory/${this.selected}?page=${page}`
          );
        }
        this.products = dataProducts.data;
        this.currentPage = dataProducts.current_page;
        this.totalPages = dataProducts.last_page;

      } catch (e) {
        console.log(e);
      } finally {
        this.loading = false;
      }
    },
    changeSelected(id){
      this.selected=id;
      this.loadProducts(1)
    }


  },
}
</script>


