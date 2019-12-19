<template>
  <card type="plain" title="Carte">
    <div id="map" class="map"></div>
  </card>
</template>
	
<script>
import axios from "axios";

export default {
  data() {
      return {
          objData : [],
      }
  },
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
  },
  created() {
      axios
        .get(`http://localhost:3000/interventions/`)
        .then(response => {
          this.objData = response.data
          console.log(this.objData)
        })
        .catch(e => {
          console.log('ca passe pas bill')
        })
    },

};
</script>
