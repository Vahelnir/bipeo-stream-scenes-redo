<script setup lang="ts">
import { onMounted, useTemplateRef } from "vue";
import { useRouter } from "vue-router";

import BigLoader from "../components/big-loader.vue";
import { wait } from "../utils/wait";

const router = useRouter();

const wrapperElement = useTemplateRef("wrapper");

onMounted(async () => {
  if (!wrapperElement.value) return;

  await wait(3000);
  const animation = wrapperElement.value?.animate(
    [
      { "--gradient-progress": "0%", opacity: 1 },
      { "--gradient-progress": "320%", opacity: 1, offset: 0.95 },
      { "--gradient-progress": "320%", opacity: 0 },
    ],
    {
      duration: 12000,
      fill: "forwards",
    },
  );
  animation.commitStyles();
  await animation.finished;

  await router.push({ name: "/start-screen" });
});
</script>

<template>
  <div class="bg-white w-full h-full">
    <div
      ref="wrapper"
      class="flex justify-center items-center h-full w-full wrapper"
      style="--gradient-progress: 0%"
    >
      <BigLoader class="spin-animation" />
    </div>
  </div>
</template>

<style scoped>
@property --gradient-progress {
  syntax: "<percentage>";
  inherits: false;
  initial-value: 0%;
}

.wrapper {
  background: linear-gradient(
    45deg,
    var(--color-bipeo-dark-blue) calc(100% - var(--gradient-progress)),
    transparent calc(400% - var(--gradient-progress))
  );
}

.spin-animation {
  animation:
    spin 15s linear infinite,
    fade-in 0.4s ease-in forwards;
}

@keyframes fade-in {
  0% {
    opacity: 0;
  }
  100% {
    opacity: 1;
  }
}

@keyframes spin {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}
</style>
