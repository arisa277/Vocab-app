<template>
  <div class="container">
    <div class="body">
    <h1>Vocab-App</h1>
    <div class="link-area">
      <p><nuxt-link to="/questions/day">Day</nuxt-link></p>
      <p><nuxt-link to="#">Month</nuxt-link></p>
      <p><nuxt-link to="#">Number</nuxt-link></p>
      <p><nuxt-link to="">Time attack</nuxt-link></p>
    </div>
    </div>
  </div>
</template>

<script>
export default {}
</script>

<style>
.container{
  background: #aac9ce;
  margin: 0 auto;
  height: 100vh;
  text-align: center;
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>
