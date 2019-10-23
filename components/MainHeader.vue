<template>
  <header class="main-header">
    <nav class="navbar navbar-expand-lg navbar-dark bg-dark">
      <div class="container">
        <nuxt-link class="navbar-brand" to='/'>WP Headless</nuxt-link>
        <button class="navbar-toggler">
          <span class="navbar-toggler-icon"></span>
        </button>

        <div class="collapse navbar-collapse">
          <ul class="navbar-nav mr-auto">
            <li class="nav-item">
              <nuxt-link class="nav-link" exact-active-class="active" to="/">الرئيسية</nuxt-link>
            </li>
            <li class="nav-item">
              <nuxt-link class="nav-link" exact-active-class="active" to="/blog">المدونة</nuxt-link>
            </li>
          </ul>
        </div>
      </div>
    </nav>
  </header>
</template>

<script>
export default {
  name: "MainHeader"
};
</script>

<style>
</style>
