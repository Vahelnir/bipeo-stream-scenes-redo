<script setup lang="ts">
import DashBorderOverlay from "../components/dash-border-overlay.vue";
import DatetimeIndicator from "../components/datetime-indicator.vue";
import Measurement from "../components/measurement.vue";
import MusicPlayer from "../components/music-player.vue";
import UserMessages from "../components/user-messages.vue";
import WelcomeStreamModal from "../components/welcome-screen/welcome-stream-modal.vue";

import MdiTwitter from "~icons/mdi/twitter";
</script>

<template>
  <DashBorderOverlay>
    <MusicPlayer class="absolute top-3 left-24 max-w-100" />
    <DatetimeIndicator class="absolute top-3 right-24 w-60" />
    <div class="absolute bottom-5.5 left-24 w-44">
      <div
        class="flex h-6 justify-center gap-3 rounded-lg bg-[#030636] px-2 font-bold"
      >
        <MdiTwitter class="mt-0.5" /> @Copypeo_dev
      </div>
    </div>

    <UserMessages />

    <WelcomeStreamModal class="absolute inset-0 z-10 m-auto" />

    <Measurement v-if="false" />
  </DashBorderOverlay>
</template>
