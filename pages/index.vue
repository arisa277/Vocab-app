<template>
  <div class="container">
    <div class="body">
      <h1>Swedish Typing-App</h1>
      <p class="description">Click the course!</p>
      <div class="link-area">
        <p>Practice:<nuxt-link to="/questions/day">Day</nuxt-link></p>
        <p><nuxt-link to="/questions/month">Month</nuxt-link></p>
        <p>Test:<nuxt-link to="questions/timeAttack">Time Attack</nuxt-link></p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {};
  }
};
</script>

<style>
* {
  font-family: Cambria, Cochin, Georgia, Times, "Times New Roman", serif;
}
h1 {
  color: #49634b;
  margin: 10px 0;
}
.description {
  color: rgba(0, 0, 0, 0.7);
  font-size: 20px;
  font-weight: bold;
}
.container {
  background: #ded2c2;
  margin: 0 auto;
  height: 100vh;
  text-align: center;
  display: flex;
  justify-content: center;
  align-items: center;
}
.link-area {
  display: flex;
  margin: 20px auto;
  justify-content: center;
  padding: 5px;
}
.link-area a {
  border: 1px solid rgba(0, 0, 0, 0.7);
  padding: 10px;
  border-radius: 2px;
  color: rgba(0, 0, 0, 0.7);
  margin: 0px 7px;
  text-decoration: none;
}
.link-area a:hover {
  background: #49634b;
  opacity: 0.7;
  color: #fff;
  border: 1px solid #fff;
}
</style>
