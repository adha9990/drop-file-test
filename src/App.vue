<script setup>
import DropZoneVue from "./components/DropZoneVue.vue";

const onDrop = (files) => {
  console.log(files);
};
</script>

<template>
  <div class="app">
    <DropZoneVue @onDrop="onDrop">
      <div class="test"></div>
    </DropZoneVue>
  </div>
</template>

<style lang="scss" scoped>
.app {
  height: 100%;
  .test {
    width: 500px;
    height: 300px;
    background-color: red;
    float: right;
    &:hover {
      background-color: blue;
    }
  }
}
</style>
