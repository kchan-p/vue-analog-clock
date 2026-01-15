/** * 文字盤の描画 */
<script setup>
import ClockFaceFrame from "./frame.vue";
import ClockFaceScale from "./scale.vue";
import ClockFaceText from "./text.vue";
import ClockFaceCenter from "./center.vue";

const props = defineProps(["radius"]);

</script>

<template>
  <ClockFaceFrame />
  <ClockFaceScale :radius="props.radius" />
  <ClockFaceText :radius="props.radius" />
  <ClockFaceCenter />
</template>
