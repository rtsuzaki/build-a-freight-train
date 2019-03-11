<template>
  <div class="container">
    <div class="holder">
      <form @submit.prevent="$emit('add-wagon')">
        <div class="field">
          <label>Select Wagon Type To Add:</label>
          <select @change="$emit('select-wagon', $event)">
            <option disabled value="">Please select one</option>
            <option>Open Wagon</option>
            <option>Covered Wagon</option>
            <option>Flat Wagon</option>
            <option>Tank Wagon</option>
          </select>
        </div>

        <div class="field">
          <label>Select Wagon Subtype (No subtype for open and flat wagons):</label>
          <select v-if="wagonSelected === 'Covered Wagon'" @change="$emit('select-subtype', $event)">
            <option disabled value="">Please select one</option>
            <option value="Regular">Regular</option>
            <option value="Refrigerated">Refrigerated</option>
            <option value="Livestock">Livestock</option>
          </select>
          <select v-else-if="wagonSelected === 'Tank Wagon'" @change="$emit('select-subtype', $event)">
            <option disabled value="">Please select one</option>
            <option value="Liquid">Liquid</option>
            <option value="Gas">Gas</option>
            <option value="Refrigerated Liquid">Refrigerated Liquid</option>
            <option value="Refrigerated Gas">Refrigerated Gas</option>
          </select>
          <select v-else size="1" @change="$emit('select-subtype', $event)">
            <option disabled value="">Please select one</option>
            <option value="None">None</option>
          </select>
        </div>
        <button type="submit" class="wagon-btn">Add Selected Wagon</button>
      </form>
      <button class="wagon-btn" v-on:click="$emit('remove-wagon')">Remove Last Wagon</button>
      <button v-on:click="$emit('submit-train')" id="submit-btn">Submit Constructed Train</button>
      
    </div>
  </div>
</template>

<script>

export default {
  name: 'AddWagonForm',
  props: ['trains', 'wagonSelected','subtypeSelected'],
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

  .holder {
    background: #fff;
    padding:10px;
  }

  .container {
    box-shadow: 0px 0px 40px lightgray;
  }

  select {
    display:block;
  }

  .field {
    display: block;
    margin: 20px;
  }

  label {
    font-weight:bold;
    font-size: 18px;
  }

  .wagon-btn {
    display: inline-block;
    margin: 20px;
    padding:10px;
  }

  #submit-btn {
    background-color: green;
    border: none;
    color: white;
    font-size: 16px;
    margin: 20px;
    padding: 10px;
    border-radius: 5px;
  }
</style>
