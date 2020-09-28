<template>
  <div id="app">
    <div>{{ info }}</div>
    <GmapMap
      :center="{ lat: 30, lng: 120 }"
      :zoom="7"
      map-type-id="terrain"
      style="width: 100%; height: 800px"
    >
      <GmapMarker
        :key="index"
        v-for="(m, index) in markers"
        :position="m.position"
        :clickable="true"
        :draggable="true"
        @click="center = m.position"
      />
    </GmapMap>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "App",
  components: {},
  data() {
    return {
      markers: [{ position: { lat: 31, lng: 121 } }],
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
