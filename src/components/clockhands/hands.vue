/** * 針の描画 */
<script setup>
import { ref, onMounted, onBeforeUnmount, computed } from "vue";
import ClockHand from "./hand.vue";

const props = defineProps(["radius"]);

const d = new Date();
const hour = ref(d.getHours());
const minute = ref(d.getMinutes());
const second = ref(d.getSeconds());

const hourValue = computed(() => (hour.value % 12) * 60 + minute.value);

let timeoutId;

onMounted(() => {
  const schedule = () => {
    const delay = 1000 - (Date.now() % 1000);

    timeoutId = window.setTimeout(() => {
      const now = new Date();
      hour.value = now.getHours();
      minute.value = now.getMinutes();
      second.value = now.getSeconds();
      schedule();
    }, delay);
  };

  schedule();
});

onBeforeUnmount(() => {
  clearTimeout(timeoutId);
});
</script>
<template>
  <ClockHand id="hand-hour" :radius="props.radius" :value="hourValue" :divNum="720" />
  <ClockHand id="hand-minute" :radius="props.radius" :value="minute" :divNum="60" />
  <ClockHand id="hand-second" :radius="props.radius" :value="second" :divNum="60" />
</template>
