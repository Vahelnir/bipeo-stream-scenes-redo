<script setup lang="ts">
import { ref } from "vue";

const x = ref(50);
const y = ref(700);
const width = ref(1500);
const height = ref(150);
</script>

<template>
  <div
    ref="el"
    class="bg-red-200"
    :style="{
      width: `${Math.round(width)}px`,
      height: `${Math.round(height)}px`,
      left: `${Math.round(x)}px`,
      top: `${Math.round(y)}px`,
    }"
    style="position: absolute"
  >
    {{ Math.round(x) }} x {{ Math.round(y) }}
  </div>
</template>
