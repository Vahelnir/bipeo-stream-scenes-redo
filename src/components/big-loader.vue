<script setup lang="ts">
import { roundDecimals } from "../utils/round-decimals";

const CIRCLE_START_ANGLE = 180;

withDefaults(
  defineProps<{
    activeCircles?: number;
  }>(),
  {
    activeCircles: 8,
  },
);

function circleStyle(index: number, total: number, radius: number) {
  const angle = CIRCLE_START_ANGLE + ((index - 1) * 360) / total;
  const rad = (angle * Math.PI) / 180;
  const cosX = roundDecimals(Math.cos(rad), 2);
  const sinY = roundDecimals(Math.sin(rad), 2);
  const x = cosX * radius;
  const y = sinY * radius;
  return {
    left: `calc(50% + ${x}px - 1.2rem)`,
    top: `calc(50% + ${y}px - 1.2rem)`,
    "--circle-translate-x": cosX,
    "--circle-translate-y": sinY,
  };
}
</script>

<template>
  <div ref="loaderElement" class="relative opacity-100 w-100 h-100">
    <div
      v-for="i in 8"
      :key="i"
      class="absolute rounded-full h-10 w-10 transition-transform ease-in-out"
      :class="{
        'bg-white/25': activeCircles < i,
        'bg-white circle-active': activeCircles >= i,
      }"
      :style="circleStyle(i, 8, 10 * 16)"
    ></div>
  </div>
</template>

<style scoped>
.circle-active {
  transform: translate(
    calc(var(--circle-translate-x) * 2em),
    calc(var(--circle-translate-y) * 2em)
  );
}
</style>
