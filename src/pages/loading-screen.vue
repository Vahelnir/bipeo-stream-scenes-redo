<script setup lang="ts">
import { ref } from "vue";
import { useAnimate } from "@vueuse/core";

import DashBorderOverlay from "../components/dash-border-overlay.vue";

const loaderElement = ref<HTMLElement | undefined>();
useAnimate(
  loaderElement,
  [
    { opacity: 0, transform: "translateX(0%)" },
    { opacity: 0, transform: "translateX(0%)", offset: 0.5 },
    { opacity: 1, transform: "translateX(0%)", offset: 0.6 },
    { opacity: 1, transform: "translateX(0%)", offset: 0.9 },
    { opacity: 1, transform: "translateX(100%)" },
  ],
  { duration: 3000, easing: "ease-in-out", fill: "forwards" },
);

function circleStyle(index: number, total: number, radius: number) {
  const angle = ((index - 1) * 360) / total;
  const rad = (angle * Math.PI) / 180;
  const x = Math.cos(rad) * radius;
  const y = Math.sin(rad) * radius;
  return {
    left: `calc(50% + ${x}px - 1.2rem)`,
    top: `calc(50% + ${y}px - 1.2rem)`,
  };
}
</script>

<template>
  <DashBorderOverlay>
    <div ref="loaderElement" class="loader absolute inset-0 m-auto w-100 h-100">
      <div
        v-for="i in 8"
        :key="i"
        class="absolute bg-white/25 rounded-full h-10 w-10"
        :style="circleStyle(i, 8, 10 * 16)"
      ></div>
    </div>
  </DashBorderOverlay>
</template>
