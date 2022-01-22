<template>


<h1>Poker Charts - Preflop</h1>

<div class="chart-btns">

  <rfiLJ/>

<!-- RFI-POS  -->
  <div class="buttons">
    <span
      id="title"
      style="font-size: 15px;"
    >
    RFI / POSITION
    </span>
    <span
      style="font-size: 30px;"
      @click="handleClick(pos, index)"
      v-for="(pos, index) in RFIPOS"
      :key="pos"
    >
    {{ pos }}
    </span>
  </div>

<!-- vs RFI -->
  <div class="buttons">
    <span
      id="title"
      style="font-size: 24px;"
      v-if="this.vsrfi.length > 0"
    >
    vs RFI
    </span>
    <span
      style="font-size: 18px; "
      @click="handleClick(vsrfi, index)"
      v-for="vsrfi in vsrfi"
      :key="vsrfi"
    >{{ vsrfi }}</span>
  </div>


<!-- vs3bet -->
  <div class="buttons">
    <span
      id="title"
      style="font-size: 24px;"
      v-if="this.vs3bet.length > 0"
    >
    vs 3bet
    </span>
    <span
      style="font-size: 16px;"
      @click="handleClick(vs3bet, index)"
      v-for="vs3bet in vs3bet"
      :key="vs3bet"
    >{{ vs3bet }}</span>
  </div>


</div>

</template>

<script>
import chart from "./components/chart.vue"
import rfiLJ from "./components/rfi-lj.vue"

export default {
  name: "App",
  components: { chart, rfiLJ
  },
  data() {
    return {
      selected: null,
      RFIPOS: ["LJ","HJ","CO","BTN","SB","BB",],
      vsrfi: [],
      vs3bet: []
    }
  },
  methods: {
    handleClick(val, index) {

      // "vs HJ 3bet","vs CO 3bet","vs BTN 3bet","vs SB 3bet","vs BB 3bet"

      this.selected = val

      // LJ
      if (this.selected === "LJ") {
        this.vsrfi = [];
        this.vs3bet = ["vs HJ 3bet"]
      }
      // HJ
      if (this.selected === "HJ") {
        this.vsrfi = ['vs LJ RFI'];
        this.vs3bet = ["vs CO 3bet","vs BTN 3bet","vs SB 3bet","vs BB 3bet"]
      }
      // CO
      if (this.selected === "CO") {
        this.vsrfi = ['vs LJ RFI','vs HJ RFI']
        this.vs3bet = ["vs BTN/SB 3bet","vs BB 3bet"]
      }
      // BTN
      if (this.selected === "BTN") {
        this.vsrfi = ["vs LJ RFI","vs HJ RFI","vs CO RFI"]
        this.vs3bet = ["vs BB/SB 3bet"]
      }
      // SB
      if (this.selected === "SB") {
        this.vsrfi = ["vs LJ RFI","vs HJ RFI","vs CO RFI", "vs BTN RFI"]
        this.vs3bet = ["vs BB 3bet"]
      }
      // BB
      if (this.selected === "BB") {
        this.vsrfi = ["vs LJ RFI","vs HJ RFI","vs CO RFI","vs BTN RFI","vs SB Limp","vs SB Raise",]
        this.vs3bet = []
      }

      console.log(this.selected)
    }
  }


};
</script>

<style>

#app {
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
}

.chart-btns {
  display: flex;
}

.buttons {
  display: flex;
  flex-direction: column;
}

.buttons span {
  cursor: pointer;
  background-color: rgb(204, 16, 16);
  color: rgb(231, 231, 231);
  width: 100px;
  height: 40px;
  margin: 0 5px 10px 10px;
  display: flex;
  justify-content: space-around;
  align-items: center;
  text-align: center;
}

#title {
  background-color: rgb(10, 114, 10);
  text-align: center;
  cursor: default;
}

</style>
