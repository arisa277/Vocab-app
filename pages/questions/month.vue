<template>
  <div class="">
      <Question :qas="qas" title="Månad"/>
  </div>
</template>

<script>
export default {
  data() {
    return {
      qas: [
        {
          q: "January",
          a: "januari"
        },
        {
          q: "February",
          a: "februari"
        },
        {
          q: "March",
          a: "mars"
        },
        {
          q: "April",
          a: "april"
        },
        {
          q: "May",
          a: "maj"
        },
        {
          q: "June",
          a: "juni"
        },
        {
          q: "July",
          a: "juli"
        },
        {
          q: "August",
          a: "augusti"
        },
        {
          q: "September",
          a: "september"
        },
        {
          q: "October",
          a: "oktober"
        },
        {
          q: "November",
          a: "november"
        },
        {
          q: "December",
          a: "december"
        },
      ]
    };
  }
};
</script>
