<template>

  <background/>

  <settings/>

<div class="main">

  <p class="main-title">Preflop 6max Cash 100bb NLHE</p>

  <p class="situation-title">{{ this.situation ? this.situation : 'Choose a Situation Below' }}</p>

  <chart :situation="situation"/>

  <buttons @change="handleSituation"/>

</div>
</template>

<script>
import chart from "./components/chart.vue"
import buttons from "./components/buttons.vue"
import background from "./components/background.vue"
import settings from "./components/settings.vue"


export default {
  name: "App",
  components: { chart, buttons, background, settings },
  data() {
    return {
      situation: ''
    }
  },
  methods: {
    handleSituation(situation) {
      this.situation = situation
    }
  }
};
</script>

<style>
  * {
    padding: 0;
    margin: 0;
    /* background-color: rgb(34, 34, 34); */
  }

  #app {
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
    /* display: flex;
    flex-direction: column;
    align-items: center; */
    height: 100vh;
    user-select: none;
    /* background-color: rgb(34, 34, 34); */
  }

  .main {
    transform: scale(1);
    display: flex;
    flex-direction: column;
    align-items: center;
  }

  .main-title {
    font-size: 26px;
    margin: 20px 0 20px 0;
    color: white;
    text-align: center;
  }

  .situation-title {
    background-color: rgb(10, 114, 10);
    color: white;
    padding: 5px;
    text-align: center;
    margin-bottom: 5px;
  }

</style>