<script setup>
import DropZoneVue from "./components/DropZoneVue.vue";

const onDrop = (files) => {
  console.log(files);
};
</script>

<template>
  <DropZoneVue class="app" @onDrop="onDrop"></DropZoneVue>
</template>

<style lang="scss">
.app {
  height: 100%;
}
</style>
