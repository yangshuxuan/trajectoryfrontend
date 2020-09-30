<template>
  <div class="fill" id="map" ref="map">

      <MapMarker
        :key="index"
        v-for="(m, index) in markers"
        :objectInfo="m"
        :lat="m.lat"
        :lng="m.lng"
      />

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
    markers: [
      {
        object_id: "1",
        lastmodified_time: "2020-09-23 16:11:00",
        long: 120.036,
        lat: 31.344,
      },
    ],
    intervalid1: null,
  }),
  methods: {
    todo: function () {
      let vm = this;
      this.intervalid1 = setInterval(function () {
        console.log("hi");
        axios({
          method: "GET",
          url: "http://127.0.0.1:5002/lastappeared",
        })
          .then((response) => {
            console.log(response.data[0]);
            vm.markers = response.data;
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
      center: { lat: 31.1, lng: 120.01 },
      zoom: 7,
    });
  },
  beforeDestroy() {
    clearInterval(this.intervalid1);
  },
};
</script>

<style scoped>


.fill {
  /* min-height: 100%; */
  
  min-width: 100%;
  width: 100%;
  height: calc(100vh - 60px);
  display: flex;
}

</style>