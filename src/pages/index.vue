<script setup lang="ts">
import { useNow } from "@vueuse/core";
import { computed } from "vue";
import WelcomeStreamModal from "../components/welcome-stream-modal.vue";

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
  <div class="h-dvh w-dvw bg-[#030636] px-2">
    <div
      class="grid-background-animated relative flex h-full w-full items-center justify-center overflow-hidden text-white"
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
          height="172"
          rx="6"
          fill="none"
          stroke="#fff"
          stroke-width="1"
          stroke-dasharray="180 80 140 80"
          stroke-linecap="butt"
        />
      </svg>
      <div
        class="absolute top-2 left-24 max-w-100 rounded-lg bg-[#030636] px-4 font-bold"
      >
        wii party - nintendo lofi
      </div>
      <div
        class="absolute top-2 right-24 w-60 rounded-lg bg-[#030636] px-4 text-center font-bold"
      >
        {{ formattedTime }}
      </div>

      <WelcomeStreamModal />
    </div>
  </div>
</template>

<style scoped>
.grid-background-animated {
  background-image:
    url("data:image/svg+xml,%3Csvg width='50' height='50' viewBox='0 0 40 40' fill='none' xmlns='http://www.w3.org/2000/svg'%3E%3Crect x='0' y='0' width='40' height='40' fill='none'/%3E%3Cpath d='M 40 0 H 0 V 40' stroke='black' stroke-width='2'/%3E%3C/svg%3E"),
    radial-gradient(transparent, #030636);
  background-color: #030636;
  background-repeat: repeat;
  background-size: 50px 50px;
  animation: background-animation 15s linear infinite;

  > svg {
    background-image: radial-gradient(
      circle,
      rgba(3, 6, 54, 0) 0%,
      rgba(3, 6, 54, 1) 90%
    );
  }
}

.border-animation rect {
  animation: dash-animation 20s ease-in-out infinite alternate;
}

@keyframes dash-animation {
  from {
    stroke-dashoffset: 60;
  }
  to {
    stroke-dashoffset: 80;
  }
}

@keyframes background-animation {
  from {
    background-position: 0 0;
  }
  to {
    background-position: 200px 100px;
  }
}
</style>
