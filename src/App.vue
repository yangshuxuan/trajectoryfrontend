<template>
  <div id="app">
    <!-- <Navbar2 />
    <RealTimeMap/> -->
    <testtooltip/>
    <testfrom/>
    
  </div>
</template>

<script>
import axios from "axios";

// import Navbar2 from './components/Navbar2.vue'; 
// import RealTimeMap from "./components/RealTimeMap"
import testtooltip from "./components/testtooltip"
import testfrom from "./components/testfrom"
export default {
  name: "App",
  components: {

    // RealTimeMap,
    // Navbar2,
    testtooltip,
    testfrom

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
  width: 100%;
  height: 100%;
  margin: 0;
}
body, html {
  height: 100%;
  width: 100%;
  margin: 0;
}
</style>
