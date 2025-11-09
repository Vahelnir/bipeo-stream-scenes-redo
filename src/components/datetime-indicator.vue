<script setup lang="ts">
import { computed } from "vue";
import { useNow } from "@vueuse/core";

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
  <div class="h-6 rounded-lg bg-[#030636] px-4 text-center font-bold">
    {{ formattedTime }}
  </div>
</template>
