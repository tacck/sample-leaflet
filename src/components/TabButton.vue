<template>
  <span class="tab-button">
    <b-button @click="$emit('click')" size="lg" :variant="status">{{
      label
    }}</b-button>
  </span>
</template>

<script>
export default {
  props: {
    label: {
      type: String,
      required: true
    },
    status: {
      type: String,
      default: ""
    }
  }
};
</script>

<style>
.tab-button {
  margin: 10px;
}
</style>
