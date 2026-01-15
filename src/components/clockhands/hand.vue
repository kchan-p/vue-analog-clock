/**
* 針の描画
*/
<script setup>
import { ref, onMounted, computed } from "vue";

const HandLengthPerProp = "--react-analog-clock-handlengthper";
const HandGapPerProp = "--react-analog-clock-handgapper";

const props = defineProps(["id", "radius", "value", "divNum"]);
const width = ref(0);
const handLengthPer = ref(0);
const handGapPer = ref(0);

const handRef = ref(null);

onMounted(() => {
  const style = window.getComputedStyle(handRef.value);
  const lengthPer = Number(style.getPropertyValue(HandLengthPerProp));
  const gapPer = Number(style.getPropertyValue(HandGapPerProp));
  if (!isNaN(lengthPer)) handLengthPer.value = lengthPer;
  if (!isNaN(gapPer)) handGapPer.value = gapPer;
  width.value = handRef.value.clientWidth;
});

const style = computed(() => {
  const radius = props.radius;
  const handLength = (radius * handLengthPer.value) / 100;
  const handGap = (radius * handGapPer.value) / 100;
  const angle = 360 / props.divNum;

  return {
    height: handLength + handGap + "px",
    top: radius - handLength + "px",
    left: radius - width.value / 2 + "px",
    transformOrigin: `center ${handLength}px `,
    transform: `rotate(${angle * props.value}deg)`
  };
});

</script>
<template>
  <div :id="props.id" :style="style" ref="handRef"></div>
</template>
