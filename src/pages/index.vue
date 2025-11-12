<script setup lang="ts">
import { useCurrentElement } from "@vueuse/core";
import { useRouter } from "vue-router";

import DashBorderOverlay from "../components/dash-border-overlay.vue";
import DatetimeIndicator from "../components/datetime-indicator.vue";
import Measurement from "../components/measurement.vue";
import MusicPlayer from "../components/music-player.vue";
import UserMessages from "../components/user-messages.vue";
import WelcomeStreamModal from "../components/welcome-screen/welcome-stream-modal.vue";

import MdiTwitter from "~icons/mdi/twitter";

const TIMER_DURATION = 10;

const router = useRouter();
const rootElement = useCurrentElement<HTMLElement>();

async function nextPage() {
  await rootElement.value?.animate([{ opacity: 1 }, { opacity: 0 }], {
    duration: 1000,
    fill: "forwards",
  }).finished;
  return router.push({ name: "/startup" });
}
</script>

<template>
  <DashBorderOverlay>
    <MusicPlayer class="absolute top-3 left-24 max-w-100" />
    <DatetimeIndicator class="absolute top-3 right-24 w-60" />
    <div class="absolute bottom-3.5 left-24 w-44">
      <div
        class="flex h-6 justify-center gap-3 rounded-lg bg-bipeo-dark-blue px-2 font-bold"
      >
        <MdiTwitter class="mt-0.5" /> @Cloneo_dev
      </div>
    </div>

    <UserMessages />

    <WelcomeStreamModal
      :duration="TIMER_DURATION"
      @timerEnded="nextPage"
      class="absolute inset-0 z-10 m-auto"
    />

    <Measurement v-if="false" />
  </DashBorderOverlay>
</template>
