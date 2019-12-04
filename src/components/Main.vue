<template>
  <div class="content">
    <Tab @changeActive="setActive"></Tab>
    <Map :lat="lat" :lon="lon"></Map>
  </div>
</template>

<script>
import Tab from "./Tab";
import Map from "./Map";

export default {
  components: {
    Tab,
    Map
  },
  data: function() {
    return {
      geosObject: {},
      staticLatitude: 43.0680165,
      staticLongitude: 141.3519007,
      currentLatitude: 40,
      currentLongitude: 120,
      lat: 0,
      lon: 0
    };
  },
  mounted: function() {
    // 現在位置を設定
    if (navigator.geolocation) {
      navigator.geolocation.getCurrentPosition(this.setCurrentPosition);
      navigator.geolocation.watchPosition(this.setCurrentPosition);
    }

    // 切り替え用の位置情報配列作成
    this.geosObject.static = [this.staticLatitude, this.staticLongitude];
    this.geosObject.current = [this.currentLatitude, this.currentLongitude];

    this.setActive("static");
  },
  methods: {
    setActive: function(location) {
      this.lat = this.geosObject[location][0];
      this.lon = this.geosObject[location][1];
    },
    setCurrentPosition: function(position) {
      this.geosObject.current = [
        position.coords.latitude,
        position.coords.longitude
      ];
    }
  }
};
</script>

<style>
.content {
  height: 100%;
  display: grid;
  grid-template-rows: auto 1fr;
}
</style>
