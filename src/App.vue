<template>


  <div class="main-app">
    <!-- SETTINGS -->
    <settings
      @change="handleOrientation"
    />
    <!-- MAIN TITLE -->
    <p class="main-title">Preflop 6max Cash 100bb NLHE</p>
    <div
      class="title-chart"
      :style="`flex-direction: ${currentOrientation};`"
    >
      <div>
        <!-- SITUATION TITLE -->
        <p class="situation-title">{{ this.situation ? this.situation : 'Choose a Situation Below' }}</p>
        <!-- CHART -->
        <chart :situation="situation"/>
      </div>
      <!-- BUTTONS -->
      <buttons @change="handleSituation"/>
    </div>
  </div>

  <!-- BACKGROUND -->
  <background/>

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
      situation: '',
      currentOrientation: 'column',
      currentSize: 0
    }
  },
  methods: {
    handleSituation(situation) {
      this.situation = situation
    },
    handleOrientation(orientation) {
      this.currentOrientation = orientation;
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
    height: 100vh;
    user-select: none;
  }

  .main-app {
    height: 100vh;
    display: flex;
    flex-direction: column;
    align-items: center;
    
  }

  .title-chart {
    display: flex;
    align-items: center;
  }

  .main-title {
    font-size: 26px;
    margin-bottom: 20px;
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