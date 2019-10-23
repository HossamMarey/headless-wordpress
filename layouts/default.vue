<template>
  <div>
    <MainHeader />
    <nuxt />
    <div class="main-info">
      <small>this Blog for test Headless Wp REST API</small>
    </div>

  </div>
</template>

<script>
import MainHeader from "../components/MainHeader";
export default {
  components: { MainHeader }
};
</script>

<style>
html {
  font-family: 'Cairo', sans-serif;
  font-size: 16px;
  word-spacing: 1px;
  -ms-text-size-adjust: 100%;
  -webkit-text-size-adjust: 100%;
  -moz-osx-font-smoothing: grayscale;
  -webkit-font-smoothing: antialiased;
  box-sizing: border-box;
  direction: rtl;
}
body {
  font-family: 'Cairo', sans-serif;
  background-color: rgb(237, 233, 241);
  text-align: right;
}

*,
*:before,
*:after {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
.main-info {
  display: flex;
  flex-direction: column;
  justify-content: center;
  text-align: center;
  margin-top: 30px;
  padding: 20px;
  border-top: 1px solid rgb(216, 216, 221);
  background-color: #fff;
  box-shadow: 0 -2px 6px rgba(58, 56, 75, 0.082);
}
</style>
