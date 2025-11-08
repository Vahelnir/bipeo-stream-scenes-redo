<script setup lang="ts">
import { useNow } from "@vueuse/core";
import { computed } from "vue";
import Modal from "../components/modal.vue";

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
  <div class="grid-bg">
    <div
      class="relative h-dvh w-dvw text-white overflow-hidden flex items-center justify-center"
    >
      <svg
        class="border-animation absolute inset-0"
        viewBox="0 0 320 180"
        preserveAspectRatio="none"
      >
        <rect
          x="4"
          y="4"
          width="312"
          height="152"
          rx="6"
          fill="none"
          stroke="#fff"
          stroke-width="1"
          stroke-dasharray="180 80 140 80"
          stroke-linecap="butt"
        />
      </svg>
      <div
        class="absolute left-24 top-2 rounded-lg bg-[#030636] px-4 font-bold"
      >
        wii party - nintendo lofi
      </div>
      <div
        class="absolute right-24 top-2 rounded-lg bg-[#030636] px-4 font-bold"
      >
        {{ formattedTime }}
      </div>

      <div>
        <Modal />
      </div>
    </div>
  </div>
</template>

<style scoped>
.grid-bg {
  background-image:
    url("data:image/svg+xml,%3Csvg width='50' height='50' viewBox='0 0 40 40' fill='none' xmlns='http://www.w3.org/2000/svg'%3E%3Crect x='0' y='0' width='40' height='40' fill='none'/%3E%3Cpath d='M 40 0 H 0 V 40' stroke='black' stroke-width='2'/%3E%3C/svg%3E"),
    radial-gradient(transparent, #030636);
  background-color: #030636;
  background-repeat: repeat;

  > div {
    background-image: radial-gradient(
      circle,
      rgba(3, 6, 54, 0) 0%,
      rgba(3, 6, 54, 1) 90%
    );
  }
}

.border-animation rect {
  animation: dash-move 20s ease-out infinite alternate;
}

@keyframes dash-move {
  from {
    stroke-dashoffset: 60;
  }
  to {
    stroke-dashoffset: 80;
  }
}
</style>
