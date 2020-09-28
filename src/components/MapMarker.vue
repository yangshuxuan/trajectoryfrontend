<script>
export default {
  props: {
    
    objectInfo:{ type: Object, required: true }
  },
  data: () => ({
    marker: null,
  }),
  mounted() {
    this.$parent.getMap((map) => {
      this.marker = new window.google.maps.Marker({
        position: { lat: this.objectInfo.lat, lng: this.objectInfo.long },
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