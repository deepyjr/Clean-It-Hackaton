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
      objData: [],
      points: []
    };
  },
  methods: {
    carteMesCouilles() {
      var map = L.map("map", { doubleClickZoom: false }).setView(
        [48.864716, 2.349014],
        12
      );

      L.tileLayer("http://{s}.tile.osm.org/{z}/{x}/{y}.png", {
        attribution: "OSM"
      }).addTo(map);

      var heat = L.heatLayer(this.points, {
        maxZoom: 10
      }).addTo(map);
    }
  },
  mounted() {
    this.carteMesCouilles();
  },
  beforeMount() {
    axios
      .get(`http://localhost:3000/interventions/`)
      .then(response => {
        this.objData = response.data;
        console.log(this.objData);
        for (var i = 0; i < this.objData.length; i++) {
          this.points[i] = {
            lat: this.objData[i].latitude,
            lng: this.objData[i].longitude
          };
        }
        console.log(this.points);
      })
      .catch(e => {
        console.log("ca passe pas bill");
      });
  }
};
</script>
