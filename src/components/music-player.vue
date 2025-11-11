<script setup lang="ts">
import { computed, ref } from "vue";
import { useIntervalFn } from "@vueuse/core";

const fakePlaylist = [
  { artist: "Dada Jones", title: "Drunk like me", duration: 2 * 60 + 34 },
  { artist: "Curly", title: "The River", duration: 4 * 60 + 30 },
  { artist: "ghost.", title: "HIGH", duration: 3 * 60 + 40 },
];

const currentTrackIndex = ref(0);
const currentTime = ref(0);

const currentTrack = computed(() => fakePlaylist[currentTrackIndex.value]);
const progress = computed(() =>
  currentTrack.value
    ? (currentTime.value / currentTrack.value.duration) * 100
    : 0,
);

useIntervalFn(() => {
  if (!currentTrack.value) return;

  currentTime.value += 1;
  if (currentTime.value >= currentTrack.value.duration) {
    currentTime.value = 0;
    currentTrackIndex.value =
      (currentTrackIndex.value + 1) % fakePlaylist.length;
  }
}, 1000);
</script>

<template>
  <div
    class="h-6 rounded-lg bg-bipeo-dark-blue px-2 font-bold"
    v-if="currentTrack"
  >
    <div
      class="absolute top-0 h-full w-[calc(100%-(--spacing(4)))] rounded bg-[#ffffff45] transition-[clip-path] duration-1000 ease-linear"
      :style="{
        clipPath: `inset(0 ${100 - progress}% 0 0)`,
      }"
    ></div>
    <div class="truncate overflow-hidden px-2">
      {{ currentTrack.artist }} - {{ currentTrack.title }}
    </div>
  </div>
</template>
