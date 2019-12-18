<template>
  <card type="plain" title="Carte">
    <div id="map" class="map"></div>
  </card>
</template>
	<script>
export default {
  methods: {
    carteMesCouilles() {
      var map = L.map("map", { doubleClickZoom: false }).setView(
        [48.864716, 2.349014],
        5
      );

      L.tileLayer("http://{s}.tile.osm.org/{z}/{x}/{y}.png", {
        attribution: "OSM"
      }).addTo(map);

      var points = [{ lat: 48.840542852103084, lng: 2.3212051391601562 }];

      var heat = L.heatLayer(points, {
        maxZoom: 10
      }).addTo(map);
    }
  },
  mounted() {
    this.carteMesCouilles();
  }
};
</script>


<style>
</style>
