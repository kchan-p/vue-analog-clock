/**
* 目盛り数字の描画
*/
<script setup>
import { reactive, computed } from "vue";

const props = defineProps(["radius"]);
const r12 = 360 / 12;

const MathPi = Math.PI / 180;
const className = "face-text";

const texts = computed(() => {
  const radius = props.radius;
  const moziPos = radius - 30;

  return Array.from({ length: 12 }, (v, index) => {
    const deg = index * r12;
    const mojiX = radius + moziPos * Math.sin(deg * MathPi);
    const mojiY = radius - moziPos * Math.cos(deg * MathPi);

    const style = { top: mojiY + "px", left: mojiX + "px" };
    const text = index === 0 ? "12" : index.toString();

    return { index, className, style, text };
  });
});
</script>

<template>
  <div v-for="t in texts" :key="t.index" :class="t.className" :style="t.style">
    {{ t.text }}
  </div>
</template>
