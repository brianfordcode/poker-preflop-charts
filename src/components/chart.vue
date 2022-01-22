<template>




<div class="chart">
      <span
        v-for="val in handMaker"
        :key="val"
      >
      {{val}}
      </span>
</div>





</template>

<script>
export default {
  computed: {
    handMaker() {
      let cards = ["A","K","Q","J","T","9","8","7","6","5","4","3","2"];

      for (let i = 0; i < cards.length; i++) { let hand = cards[i]; return hand }

      return hand;
    },
  },




}
</script>

<style scoped>
    .chart {
        border: 1px solid black;
        margin-bottom: 20px;
        display: flex;
        /* grid-template-columns: repeat(13, 1fr); */
        width: min-content;
    }
    .chart span {
        border: 1px solid black;
        display: flex;
        justify-content: space-around;
        align-items: center;
        width: 15px;
        padding: 10px;
    }

</style>

