<template>
  <div>
    <custom-navbar/>
    <nuxt/>
  </div>
</template>

<script>
import CustomNavbar from "../components/layout/CustomNavbar";

export default {
  name: "default",
  components: {CustomNavbar},
}
</script>

<style scoped>
</style>
