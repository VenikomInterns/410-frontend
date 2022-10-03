<template>
  <section class="card shadow-lg bg-primary text-info p-5 d-flex">
    <h4 class="pb-5 fw-bolder">{{product.name}}</h4>
      <div class="ratio ratio-4x3">
        <img :src="product.images[0].url">
      </div>
    <h6 class="pt-5">Price: {{ product.price}} $</h6>
    <NuxtLink :to="{ name: 'Product',query: {product: product.id}}" target="_blank">
      <button class="btn btn-secondary rounded-5 mt-4 w-75 mx-auto fw-bolder">Show Product</button>
    </NuxtLink>
  </section>
</template>

<script>
export default {
  name:'ProductCard',
  props:{
    product: Object
  }
}
</script>
