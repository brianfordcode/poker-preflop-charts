<template>

    <div class="main-container">

    <!-- <div>{{ this.completeSituation === "BB vs HJ RFI" ? true : false }}</div> -->

    <div class="chart-btns">
    <!-- RFI-POS  -->
        <div class="buttons-container">
        <span
            class="title buttons"
            style="font-size: 15px;"
        >
        RFI / POSITION
        </span>
        <span
            class="buttons"
            :style="[this.selectedPosition === position ? 'background-color: rgb(12, 12, 167)' : '']"
            style="font-size: 30px;"
            @click="choosePosition(position)"
            v-for="(position) in RFIPOS"
            :key="position"
        >
        {{ position }}
        </span>
        </div>

    <!-- vs RFI -->
        <div class="buttons-container">
        <span
            class="title buttons"
            style="font-size: 24px;"
            v-if="this.vsrfi.length > 0"
        >
        vs RFI
        </span>
        <span
            class="buttons"
            :style="[this.selectedSituation === vsrfi ? 'background-color: rgb(12, 12, 167)' : '']"
            style="font-size: 18px; "
            @click="chooseSituation(vsrfi)"
            v-for="vsrfi in vsrfi"
            :key="vsrfi"
        >{{ vsrfi }}</span>
        </div>


    <!-- vs3bet -->
        <div class="buttons-container">
        <span
            class="title buttons"
            style="font-size: 24px;"
            v-if="this.vs3bet.length > 0"
        >
        vs 3bet
        </span>
        <span
            class="buttons"
            :style="[this.selectedSituation === vs3bet ? 'background-color: rgb(12, 12, 167)' : '']"
            style="font-size: 16px;"
            @click="chooseSituation(vs3bet)"
            v-for="vs3bet in vs3bet"
            :key="vs3bet"
        >{{ vs3bet }}</span>
        </div>
    </div>

    </div>

</template>

<script>
import chart from "./chart.vue"

export default {
  name: "App",
  components: { chart },
  data() {
    return {
      selectedPosition: '',
      selectedSituation: '',
      completeSituation: '',
      RFIPOS: ["LJ","HJ","CO","BTN","SB","BB",],
      vsrfi: [],
      vs3bet: []
    }
  },
  methods: {
    choosePosition(position) {
      
      this.selectedPosition = position;
      this.selectedSituation = null;
      this.completeSituation = position + " RFI";

      // LJ
      if (this.selectedPosition === "LJ") {
        this.vsrfi = [];
        this.vs3bet = ["vs HJ 3bet"]
      }
      // HJ
      if (this.selectedPosition === "HJ") {
        this.vsrfi = ['vs LJ RFI'];
        this.vs3bet = ["vs CO 3bet","vs BTN 3bet","vs SB 3bet","vs BB 3bet"]
      }
      // CO
      if (this.selectedPosition === "CO") {
        this.vsrfi = ['vs LJ RFI','vs HJ RFI']
        this.vs3bet = ["vs BTN/SB 3bet","vs BB 3bet"]
      }
      // BTN
      if (this.selectedPosition === "BTN") {
        this.vsrfi = ["vs LJ RFI","vs HJ RFI","vs CO RFI"]
        this.vs3bet = ["vs BB/SB 3bet"]
      }
      // SB
      if (this.selectedPosition === "SB") {
        this.vsrfi = ["vs LJ RFI","vs HJ RFI","vs CO RFI", "vs BTN RFI"]
        this.vs3bet = ["vs BB 3bet"]
      }
      // BB
      if (this.selectedPosition === "BB") {
        this.vsrfi = ["vs LJ RFI","vs HJ RFI","vs CO RFI","vs BTN RFI","vs SB Limp","vs SB Raise",]
        this.vs3bet = []
      }
    },
    chooseSituation(situation) {
      this.selectedSituation = situation
      this.completeSituation = this.selectedPosition + ' ' + situation;
    }
  }

};
</script>

<style scoped>

  .main-container {
    display: flex;
    flex-direction: column;
    align-items: center;
  }

  .chart-btns {
    display: flex;
    width: 330px;
  }

  .buttons-container {
    display: flex;
    flex-direction: column;
  }

  .buttons {
    cursor: pointer;
    background-color: rgb(204, 16, 16);
    color: white;
    width: 100px;
    height: 40px;
    margin: 5px;
    display: flex;
    justify-content: space-around;
    align-items: center;
    text-align: center;
  }

  .title {
    background-color: rgb(10, 114, 10);
    text-align: center;
    cursor: default;
    color: white;
  }

</style>
