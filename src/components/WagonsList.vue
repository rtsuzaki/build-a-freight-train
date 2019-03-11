<template>
    <ul>
        <p>This is the current construction of your train:</p>
        <li v-for="(data, index) in trains" :key='index'>
            <Wagon v-bind:data="data" v-bind:index="index" v-bind:trains="trains" v-on:move-wagon="$emit('move-wagon', {originalIndex: index, event:$event})" />
        </li>
    </ul>
</template>

<script>
import Wagon from './Wagon.vue';

export default {
    name: 'WagonsList',
    components: {
        Wagon,
    },
    props: ["trains"],
}
</script>

<style scoped>
  p {
    text-align:center;
    padding: 30px 0;
    color: gray;
  }

  ul {
    position:absolute;
    margin-bottom: 100px;
    padding: 0;
    list-style-type: none;
  }
  
  ul li {
    padding: 20px;
    font-size: 1.3em;
    background-color: lightblue;
    border-left: 5px solid darkblue;
    margin-bottom: 2px;
    color: #3E5252;
  }
</style>