<template>
  <div class="relative">
    <div
      class="absolute -top-3.5 -left-1.5 z-1 flex h-8 w-12 items-center justify-center rounded-lg border-2 bg-transparent"
    >
      X
    </div>
    <div
      class="after:content-[' '] relative -m-1 ml-12 h-8 w-[calc(100%-(--spacing(12)))] rounded-t-xl rounded-b-none border-2 border-b-0 bg-[#03073f] after:absolute after:bottom-0 after:z-1 after:block after:h-2 after:w-full after:bg-[#03073f]"
    >
      <slot name="header" />
    </div>
    <div
      class="relative flex h-full w-full flex-col items-center justify-center gap-3 rounded-xl rounded-tr-none border-2 bg-[#03073f] uppercase"
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
</template>
