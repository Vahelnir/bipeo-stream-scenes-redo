<script setup lang="ts">
import { computed, onMounted, onUnmounted } from "vue";
import { useCountdown } from "@vueuse/core";

import Modal from "../modal.vue";

const props = defineProps<{
  duration: number;
}>();

const emit = defineEmits<{
  timerEnded: [];
}>();

const { remaining, start, stop } = useCountdown(() => props.duration, {
  onComplete() {
    emit("timerEnded");
  },
});

onMounted(() => {
  start();
});

onUnmounted(() => {
  stop();
});

const formattedRemainingTime = computed(() => {
  const mins = Math.floor(remaining.value / 60)
    .toString()
    .padStart(2, "0");
  const secs = (remaining.value % 60).toString().padStart(2, "0");

  return `${mins}:${secs}`;
});

const progress = computed(
  () => ((props.duration - remaining.value) / props.duration) * 100,
);
</script>

<template>
  <Modal class="h-60 w-180">
    <p class="animate-pulse text-4xl">[ CHARGEMENT EN COURS ]</p>
    <p class="text animate-pulse uppercase">Le stream commence bientot</p>

    <template #progress>
      <div class="h-0.5 w-full bg-white">
        <div
          :style="{
            '--progress': progress + '%',
            'margin-left':
              'max(calc(var(--progress) - calc(var(--spacing) * 14)), 0px)',
          }"
          class="w-20 -translate-y-1/2 truncate bg-[#03073f] text-center text-2xl"
        >
          {{ formattedRemainingTime }}
        </div>
      </div>
    </template>
  </Modal>
</template>
