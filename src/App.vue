<script setup lang="ts">
import { useWindowSize } from "@vueuse/core";
import Index from "./pages/index.vue";
import { computed } from "vue";

const { width, height } = useWindowSize();
const dimensions = computed(() => ({
  width: 1920,
  height: 1080,
}));
const scale = computed(() => Math.min(width.value / 1920, height.value / 1080));
</script>

<template>
  <div
    :style="{
      width: `${dimensions.width}px`,
      height: `${dimensions.height}px`,
      transform: `scale(${scale})`,
      transformOrigin: 'top left',
    }"
  >
    <Index />
  </div>
</template>
