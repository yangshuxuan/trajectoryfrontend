<script>
export default {
  props: {
    // {
    //     "object_id": "1",
    //     "lastmodified_time": "2020-09-23 16:11:00",
    //     "long": 4.0,
    //     "lat": 1.0
    // }
    //objectInfo:
    lat: { type: Number, required: true },
    lng: { type: Number, required: true },
  },
  data: () => ({
    marker: null,
  }),
  mounted() {
    this.$parent.getMap((map) => {
      this.marker = new window.google.maps.Marker({
        position: { lat: this.lat, lng: this.lng },
        map: map,
      });
    });
  },
  beforeDestroy() {
    if (this.marker) {
      this.marker.setMap(null);
      window.google.maps.event.clearInstanceListeners(this.marker);
    }
  },
  render() {
    return null;
  },
};
</script>