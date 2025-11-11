<script setup lang="ts">
defineOptions({
  inheritAttrs: false,
});
</script>

<template>
  <div class="h-full w-full bg-bipeo-dark-blue px-2">
    <div
      class="grid-background-animated relative h-full w-full overflow-hidden text-white"
    >
      <div class="grid-background-animated__inside h-full w-full">
        <svg
          class="border-animation"
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
          class="absolute top-0 h-full w-full max-h-full max-w-full p-12"
          v-bind="$attrs"
        >
          <slot />
        </div>
      </div>
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

  > .grid-background-animated__inside {
    background-image: radial-gradient(circle, transparent, #030636 90%);
  }
}

@keyframes background-animation {
  from {
    background-position: 0 0;
  }
  to {
    background-position: 0 100px;
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
</style>
