<template>
  <div class="home">
    <div class="container">
      <div class="row">
        <div class="col-10">
          <p>this project to test Headless Wordpress REST API with NuxtJs</p>
          <nuxt-link class="link" to="/blog">Visit Blog Page</nuxt-link>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {};
</script>

<style scoped>
.row {
  height: 80vh;
  justify-content: center;
  align-items: center;
  text-align: center;
  font-size: 20px;
  font-weight: bold;
}
.row .link {
  color: crimson;
}
</style>
