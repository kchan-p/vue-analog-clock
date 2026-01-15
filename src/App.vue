<script setup>
import { ref, reactive, onMounted, onBeforeUnmount, computed } from "vue";
import ClockFace from "./components/clockface/face.vue";
import ClockHands from "./components/clockhands/hands.vue";
import ClockInfo from "./components/info/info.vue";
import "./App.css";

const frameRef = ref(null);
const frameRect = reactive({
  diameter: 0,
  radius: 0,
  x: 0,
  y: 0,
});

const innerStyle = computed(() => ({
  width: frameRect.diameter + "px",
  height: frameRect.diameter + "px",
  position: "absolute",
  top: frameRect.y - frameRect.radius + "px",
  left: frameRect.x - frameRect.radius + "px",
}));

let observe = null;

onMounted(() => {
  observe = new ResizeObserver(([entry]) => {
    const { width, height, left, top } = frameRef.value.getBoundingClientRect();

    frameRect.diameter = width < height ? width : height;
    frameRect.radius = frameRect.diameter / 2;
    frameRect.x = left + width / 2;
    frameRect.y = top + height / 2;
  });

  observe.observe(frameRef.value);
});

onBeforeUnmount(() => {
  observe?.disconnect();
});
</script>

<template>
  <div id="clock-wrap" ref="frameRef">
    <div v-if="frameRect.diameter" id="clock-container" :style="innerStyle">
      <ClockFace :radius="frameRect.radius" />
      <ClockHands :radius="frameRect.radius" />
    </div>
  </div>
  <ClockInfo />
</template>
