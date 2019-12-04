<template>
  <div class="tab">
    <TabButton
      @click="clickStation"
      id="sation"
      :status="stationVariant"
      label="札幌駅"
    ></TabButton>
    <TabButton
      @click="clickHere"
      id="here"
      :status="hereVariant"
      label="現在地"
    ></TabButton>
  </div>
</template>

<script>
import TabButton from "./TabButton";

export default {
  components: {
    TabButton
  },
  data: function() {
    return {
      stationVariant: "info",
      hereVariant: ""
    };
  },
  methods: {
    clickStation() {
      this.$ga.event('tab-button', 'static', 'static', 1);

      this.stationVariant = "info";
      this.hereVariant = "";

      this.$emit("changeActive", "static");
    },
    clickHere() {
      this.$ga.event('tab-button', 'current', 'current', 1);

      this.stationVariant = "";
      this.hereVariant = "info";

      this.$emit("changeActive", "current");
    }
  }
};
</script>

<style>
.tab {
  background-color: #ffffff;
  margin: 10px 0;
}
</style>
