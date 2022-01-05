<template>
  <div>
    <p class="score">Your score is {{ score }} out of {{ numberOfQ }}.</p>
    <div class="messages">
      <p v-if="score === 0">Nej...</p>
      <p v-else-if="score/numberOfQ <= 0.3">Bra!</p>
      <p v-else-if="0.4 <= score/numberOfQ <= 0.7">Jättebra!</p>
      <p v-else>Fantastiskt!</p>
    </div>
  </div>
</template>

<script>
export default {
  props: ["score", "numberOfQ"]
};
</script>

<style scoped>
.score {
  margin: 5px 0;
  font-size: 18px;
  color: #202020;
}
.messages {
  margin-bottom: 5px;
   font-family: "Courier New";
  color: #da8074;
  font-weight: bold;
  font-size: 30px;
}
</style>
