<script setup lang="ts">
import { useNow } from "@vueuse/core";
import { computed } from "vue";

const time = useNow();

const formattedTime = computed(() => {
  const timeString = time.value.toLocaleTimeString("en-GB", {
    hour: "2-digit",
    minute: "2-digit",
    second: "2-digit",
  });

  return `${timeString} - ${time.value.toLocaleDateString("en-GB")}`;
});
</script>

<template>
  <div
    class="absolute top-2 right-24 h-6 w-60 rounded-lg bg-[#030636] px-4 text-center font-bold"
  >
    {{ formattedTime }}
  </div>
</template>
