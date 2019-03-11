<template>
  <div id="app">
    <AddWagonForm 
      v-bind:trains="trains"
      v-bind:wagonSelected="wagonSelected"
      v-bind:subtypeSelected="subtypeSelected"
      v-on:select-wagon="selectWagon"
      v-on:select-subtype="selectSubtype"
      v-on:add-wagon="addWagon"
      v-on:remove-wagon="removeWagon"
      v-on:submit-train="submitTrain"
    />
    <WagonsList v-if="showWagons"
      v-bind:trains="trains"
      v-on:move-wagon="moveWagon"
    />

    <div v-if="!showWagons" id="output">
      <h1>Output JSON:</h1>
      {{ output }}
    </div>
  </div>
</template>

<script>
import AddWagonForm from './components/AddWagonForm.vue'
import WagonsList from './components/WagonsList.vue'

export default {
  name: 'app',
  components: {
    AddWagonForm,
    WagonsList,
  },
  data() {
    return {
      wagonSelected: 'Open Wagon',
      subtypeSelected: 'None',
      showWagons: true,
      output: null,
      trains: [
      ],
    }
  },
  methods: {
    moveWagon(movementInfo) {
      const origin = movementInfo.originalIndex;
      const targetIndex = movementInfo.event.event.target.elements['targetIndex'].selectedIndex;

      this.trains.splice(targetIndex, 0, this.trains.splice(origin, 1)[0]);
    },
    selectWagon(e) {
      const wagonType = e.target.value;
      this.wagonSelected = wagonType;
      if (wagonType === 'Covered Wagon') {
        this.subtypeSelected = 'Regular';
      } else if (wagonType === 'Tank Wagon') {
        this.subtypeSelected = 'Liquid';
      } else {
        this.subtypeSelected = 'None';
      }
    },
    selectSubtype(e) {
      this.subtypeSelected = e.target.value;
    },
    addWagon() {
      this.trains.push({wagon: this.wagonSelected, subtype: this.subtypeSelected})
    },
    removeWagon() {
      this.trains.pop()
    },
    submitTrain() {
      let wagons = [];
      for (let i = 0; i < this.trains.length; i++) {
        wagons.push({index: i, wagon: this.trains[i].wagon, subtype: this.trains[i].subtype})
      }
      this.output = {trainlength: this.trains.length, wagonsOnTrain: wagons}
      this.showWagons = !this.showWagons;
    },
  }
}
</script>

<style>
  body {
    background-color: #EEEEEE;
    display: grid;
    grid-template-rows: auto;
    justify-items: center;
    align-items: center;
  }
  body, html {
    margin: 0;
    height: 100%;
  }
  #app {
    position:absolute;
    top:10%;
    left:10%;
    width: 75%;
  }

  #output {
    margin: 30px;
  }
</style>
