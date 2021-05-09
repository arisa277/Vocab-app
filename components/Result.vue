<template>
  <div>
    <h1>this is a result page</h1>
    <p>Congradulations! your score is {{ score }} out of {{ numberOfQ }}.</p>
    <p v-if="score < 2">Good!</p>
    <p v-else-if="score === 2">Excellent</p>
    <p v-else-if="score === 3">Fantastic!</p>
  </div>
</template>

<script>
export default {
  props: ["score", "numberOfQ"]
};
</script>

<style scoped>

</style>