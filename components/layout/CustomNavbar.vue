<template>
  <main class="position-absolute w-100" style="z-index: 10">
    <nav class="navbar navbar-expand-lg navbar-dark bg-transparent">
      <div class="container">
        <nuxt-link :to="{ name: 'index' }" class="col-1 me-5">
          <img class="navbar-brand ratio" src="../../assets/images/logo.png"/>
        </nuxt-link>
        <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarSupportedContent"
                aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
          <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" id="navbarSupportedContent">
          <ul class="navbar-nav me-auto mb-2 mb-lg-0">
            <li class="nav-item text-center">
              <nuxt-link :to="{ name: 'index' }" class="nav-link">
                Home
              </nuxt-link>
            </li>
            <li class="nav-item text-center">
              <nuxt-link :to="{ name: 'Products' }" class="nav-link">
                Products
              </nuxt-link>
            </li>
          </ul>
          <nuxt-link :to="{ name: 'Cart' }" class="nav-link text-center">
            <div class="rounded-5 bg-secondary px-3 pt-2 pb-1">
              <h4>Favourites Cart 🛒</h4>
            </div>
          </nuxt-link>
        </div>
      </div>
    </nav>
  </main>
</template>

<script>
export default {
  name: "CustomNavbar"
}
</script>
