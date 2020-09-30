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
      const infowindow = new window.google.maps.InfoWindow({
        // 設定想要顯示的內容
        content: `
          <div id="content">
            <p id="firstHeading" class="firstHeading">好食餐廳</p>
          </div>
        `,
        // 設定訊息視窗最大寬度
        maxWidth: 200
      });
      // 在地標上監聽點擊事件
      this.marker.addListener("click", () => {
        // 指定在哪個地圖和地標上開啟訊息視窗
        infowindow.open(map, this.marker);
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