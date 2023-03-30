<script setup>
import { onMounted, onUnmounted, ref } from "vue";

const emit = defineEmits(["drop"]);

const active = ref(false);

const onDrop = (e) => {
  setInactive();
  const files = [...e.dataTransfer.files];
  emit("drop", files);
};

function setActive() {
  active.value = true;
}
function setInactive() {
  active.value = false;
}

const events = ["dragenter", "dragover", "dragleave", "drop"];

function preventDefaults(e) {
  e.preventDefault();
}

onMounted(() => {
  events.forEach((eventName) => {
    document.body.addEventListener(eventName, preventDefaults);
  });
});

onUnmounted(() => {
  events.forEach((eventName) => {
    document.body.removeEventListener(eventName, preventDefaults);
  });
});
</script>

<template>
  <div
    class="dropzone"
    :class="{ drop: active }"
    @dragenter.prevent="setActive"
    @dragover.prevent="setActive"
    @dragleave.prevent="setInactive"
    @drop.prevent="onDrop"
  >
    <slot></slot>
    <div class="test"></div>
    <div class="overlay">
      <div class="tip">將檔案拖放到這裡進行新增</div>
    </div>
  </div>
</template>

<style lang="scss" scoped>
.dropzone {
  position: relative;
  width: 100%;
  height: 100%;

  &.drop {
    .overlay {
      pointer-events: all;
      opacity: 1;
      .tip {
        display: block;
      }
    }
  }

  .overlay {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: rgba(0, 0, 0, 0.5);
    opacity: 0;
    pointer-events: none;
    .tip {
      --background: rgba(0, 114, 239, 1);
      --color: white;
      position: absolute;
      top: 90%;
      left: 50%;
      color: var(--color);
      font-size: 20px;
      width: 300px;
      line-height: 60px;
      text-align: center;
      background: var(--background);
      animation: drop-tip 0.8s linear infinite;
      display: none;
    }
  }
}

@keyframes drop-tip {
  $move: 500%;
  0% {
    transform: translateY(0) translateX(-50%);
  }
  50% {
    transform: translateY(-$move) translateX(-50%);
  }
  100% {
    transform: translateY(0) translateX(-50%);
  }
}
</style>

<style lang="scss" scoped>
.test {
  width: 500px;
  height: 300px;
  background-color: red;
  float: right;
  &:hover {
    background-color: blue;
  }
}
</style>
