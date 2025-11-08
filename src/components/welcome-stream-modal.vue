<script setup lang="ts">
import Modal from "./modal.vue";
</script>

<template>
  <Modal class="h-100 w-200">
    <p class="text-5xl">[ CHARGEMENT EN COURS ]</p>
    <p class="text-xl">Le stream commence bientot</p>

    <template #progress>
      <div class="h-0.5 w-full bg-white">
        <div class="w-fit -translate-y-1/2 bg-[#03073f] px-1">00:00</div>
      </div>
    </template>
  </Modal>
</template>
