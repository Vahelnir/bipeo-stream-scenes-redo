<script setup lang="ts">
import EntypoCross from "~icons/entypo/cross";
</script>

<template>
  <div class="animate-modal-bounce">
    <div class="relative z-0 h-full w-full">
      <div
        class="absolute -top-2 -left-2 z-1 flex h-8 w-12 items-center justify-center rounded-lg border-2 bg-[#03073f]"
      >
        <EntypoCross />
      </div>
      <div
        class="relative z-2 ml-12 h-8 w-[calc(100%-(--spacing(12)))] rounded-t-xl rounded-b-none border-2 border-b-0 bg-[#03073f] px-3 py-1 before:absolute before:bottom-px before:left-0 before:z-1 before:block before:h-1 before:w-full before:translate-y-full before:bg-[#03073f]"
      >
        <slot name="header" />
      </div>
      <div
        class="relative flex h-full w-full flex-col items-center justify-center gap-3 rounded-xl rounded-tr-none border-2 bg-[#03073f] px-4 py-2"
      >
        <slot />

        <div
          v-if="$slots.progress"
          class="absolute right-0 -bottom-1 left-0 mx-auto min-h-2 w-3/4"
        >
          <div class="absolute right-0 left-0 h-2 bg-[#03073f]"></div>
          <div class="absolute bottom-0 min-h-1 w-full px-4">
            <slot name="progress" />
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.animate-modal-bounce {
  animation: modal-bounce 6s ease-in-out infinite;
}

@keyframes modal-bounce {
  0%,
  100% {
    transform: translateY(0);
  }
  50% {
    transform: translateY(8px);
  }
}
</style>
