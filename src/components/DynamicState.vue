<template>
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
</template>
<script>
export default {
  name: 'DynamicsState',

  data: function () {
    return {
      markers: [{ position: { lat: 31, lng: 121 } }]
    }
  }
}
</script>