<template>
  <main class="position-absolute top-0 w-100 z-index-0">
    <div class="bg-dark custom-background-height d-flex flex-column justify-content-center align-items-center">

      <div class="w-50">
        <div class="ratio ratio-21x9">
          <img src="../assets/images/logo.png"/>
        </div>
      </div>

      <nuxt-link :to="{ name: 'Products' }" class="position-absolute bottom-10">
        <button class="btn btn-secondary rounded-5 px-5  fw-bolder">Start shopping</button>
      </nuxt-link>

    </div>
  </main>
</template>

<script>
export default {
  name: 'IndexPage',
}
</script>

<style scoped>
.custom-background-height{
  background-image: url("../assets/images/background.jpeg");
}

.bottom-10{
  bottom: 10%;
}

.z-index-0{
  z-index: 0;
}

</style>

