<template>
  <div id="map-container"></div>
</template>

<script>
import "leaflet/dist/leaflet.css";
import L from "leaflet";

export default {
  props: ["lat", "lon"],
  data: function() {
    return {
      map: null,
      currentCircle: null,
      currentPoint: null,
      zoom: 16
    };
  },
  mounted() {
    // 地図作成
    this.map = L.map("map-container")
      .setView([this.lat, this.lon], this.zoom)
      .addLayer(
        L.tileLayer("https://{s}.tile.osm.org/{z}/{x}/{y}.png", {
          attribution:
            'Map data &copy <a href="https://openstreetmap.org">OpenStreetMap</a>'
        })
      );
    // 現在位置へ
    setTimeout(() => {
      this.map.panTo([this.lat, this.lon]);
      this.currentCircle = L.circle([this.lat, this.lon], {
        color: "#EE3300",
        fillColor: "#EE3300",
        fillOpacity: 0.25,
        radius: 50
      }).addTo(this.map);
      this.currentPoint = L.circle([this.lat, this.lon], {
        color: "#EE3300",
        fillColor: "#EE3300",
        fillOpacity: 1,
        radius: 5
      }).addTo(this.map);
    }, 500);
  },
  methods: {
    updateCurrentPosition: async function() {
      if (this.map) {
        this.map.panTo([this.lat, this.lon]);
      }
      if (this.currentCircle) {
        this.currentCircle.setLatLng([this.lat, this.lon]);
      }
      if (this.currentPoint) {
        this.currentPoint.setLatLng([this.lat, this.lon]);
      }
    }
  },
  watch: {
    lat: function() {
      this.updateCurrentPosition();
    }
  }
};
</script>

<style>
#map-container {
  height: auto;
}

.leaflet-container {
  z-index: 0;
}
</style>
