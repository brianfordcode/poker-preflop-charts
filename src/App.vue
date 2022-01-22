<template>

<h2
  style="margin: 20px 0 20px 0;
         text-align: center;"
>
Preflop 6max Cash 100bb NLHE
</h2>

<div
  class="title"
  style="padding:5px;
         margin-bottom:5px"
>
{{ this.situation ? this.situation : 'Choose a Situation Below' }}

</div>

<chart :situation="situation"/>

<buttons @change="handleSituation"/>

</template>

<script>
import chart from "./components/chart.vue"
import buttons from "./components/buttons.vue"


export default {
  name: "App",
  components: { chart, buttons },
  data() {
    return {
      situation: ''
    }
  },
  methods: {
    handleSituation(situation) {
      this.situation = situation
    // console.log(situation)
    }
  }
};
</script>

<style>
  * {
    padding: 0;
    margin: 0;
  }

  #app {
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
    display: flex;
    flex-direction: column;
    align-items: center;
    height: 100vh;
    user-select: none;
  }
</style>