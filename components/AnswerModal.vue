<template>
   <modal name="modal-content" :width="'50%'">
      <p>The answer is {{answer}}</p>
   </modal>
</template>

<script>
export default {
  props: ["answer"]
}
</script>