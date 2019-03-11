<template>
    <div>
        {{ index }}. {{ data.wagon }}, ({{ data.subtype }})

        <form @submit.prevent="$emit('move-wagon', {index: index, event: $event})">
        <label>Move Wagon To The Following Position:</label>
        <select name="targetIndex" v-model="indexToMoveTo">
            <option v-for="(data, position) in trains" :key='position' :value='position'>{{ position }}</option>
        </select>
        <button type="submit">Move Wagon</button>
        </form>
    </div>
</template>

<script>
export default {
    name: 'Wagon',
    props: ["index", "data", "trains"],
    data() {
        return {
            indexToMoveTo: 0
        }
    },
}
</script>

<style scoped>
  label {
      font-size: 12px;
  }
  button {
      font-size: 12px;
  }
</style>