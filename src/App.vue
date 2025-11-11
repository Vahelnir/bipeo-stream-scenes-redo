<script setup lang="ts">
import { computed } from "vue";
import { useWindowSize } from "@vueuse/core";

const { width, height } = useWindowSize();
const dimensions = computed(() => ({
  width: 1920,
  height: 1080,
}));
const scale = computed(() => Math.min(width.value / 1920, height.value / 1080));
</script>

<template>
  <div
    class="bg-bipeo-dark-blue"
    :style="{
      width: `${dimensions.width}px`,
      height: `${dimensions.height}px`,
      transform: `scale(${scale})`,
      transformOrigin: 'top left',
    }"
  >
    <RouterView />
  </div>
</template>
