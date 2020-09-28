<template>
  <div id="app">
    <!-- <div>{{ info }}</div>
    <DynamicState v-if="show"></DynamicState> -->
    <RealTimeMap/>
  </div>
</template>

<script>
import axios from "axios";
//import DynamicState from './components/DynamicState'
//import Restaurants from "./components/Restaurants"
import RealTimeMap from "./components/RealTimeMap"
export default {
  name: "App",
  components: {
    //DynamicState,
    RealTimeMap,
    //Restaurants
    },
  data() {
    return {
      show:false,
      info: "hello world",
    };
  },

  mounted() {
    axios({ method: "GET", "url": "https://trajectoryanalysis.azurewebsites.net/lastappeared" })
      .then((response) => {
        console.log(response);
        this.info = response;
      })
      .catch(function (error) {
        // handle error
        console.log(error);
      });
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
