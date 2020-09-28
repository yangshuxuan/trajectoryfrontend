<template>
  <div>
    <button v-on:click="removeMarkers">RemoveMarkers</button>
    <div id="map" ref="map">
      <map-marker
        :key="index"
        v-for="(m, index) in markers"
        :lat="m.lat"
        :lng="m.lng"
      />
      <!-- <map-marker :lat="-27.344" :lng="133.036"></map-marker>
    <map-marker :lat="-26.344" :lng="132.036"></map-marker>
    <map-marker :lat="-25.344" :lng="131.036"></map-marker> -->
    </div>
  </div>
</template>

<script>
import MapMarker from "./MapMarker";
import axios from "axios";
export default {
  components: {
    MapMarker,
  },
  data: () => ({
    map: null,
    markers: [{ lat: -27.344, lng: 133.036 }],
    intervalid1: null,
  }),
  methods: {
    todo: function () {
      this.intervalid1 = setInterval(function () {
          console.log("hi")
        axios({
          method: "GET",
          url: "http://127.0.0.1:5002/lastappeared",
        })
          .then((response) => {
            console.log(response);

          })
          .catch(function (error) {

            console.log(error);
          });
      }, 3000);
    },
    removeMarkers() {
      this.markers = [];
    },
    getMap(callback) {
      let vm = this;
      function checkForMap() {
        if (vm.map) callback(vm.map);
        else setTimeout(checkForMap, 200);
      }
      checkForMap();
    },
  },
  mounted() {
    this.todo();
    this.map = new window.google.maps.Map(this.$refs["map"], {
      center: { lat: -23.444, lng: 129.036 },
      zoom: 7,
    });
    
  },
  beforeDestroy() {
    clearInterval(this.intervalid1);
  },
};
</script>

<style scoped>
#map {
  height: 600px;
  background: gray;
}
</style>