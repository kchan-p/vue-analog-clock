/** * 目盛りの描画 */
<script setup>
import { reactive, computed } from "vue";

const props = defineProps(["radius"]);

const r60 = 360 / 60;

const scales = computed(() => {
  const transformOrigin = `${props.radius}px center`;
  return Array.from({ length: 60 }, (v, index) => {
    const deg = index * r60;
    const className = index % 5 === 0 ? "face-line1" : "face-line2";
    const style = { transformOrigin };
    if (index !== 0) style.transform = `rotate(${deg}deg)`;
    return { index, className, style };
  });
});
</script>

<template>
  <div v-for="s in scales" :key="s.index" :class="s.className" :style="s.style"></div>
</template>
