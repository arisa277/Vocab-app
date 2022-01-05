<template>
  <div>
    <Question :qas="qas" title="Veckodagarna"/>
  </div>
</template>

<script>
export default {
  data() {
    return {
      qas: [
        {
          q: "Monday",
          a: "måndag"
        },
        {
          q: "Tuesday",
          a: "tisdag"
        },
        {
          q: "Wednesday",
          a: "onsdag"
        },
        {
          q: "Thursday",
          a: "torsdag"
        },
        {
          q: "Friday",
          a: "fredag"
        },
        {
          q: "Saturday",
          a: "lördag"
        },
        {
          q: "Sunday",
          a: "söndag"
        }
      ]
    };
  },
};
</script>
