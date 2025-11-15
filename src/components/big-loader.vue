<script setup lang="ts">
withDefaults(
  defineProps<{
    activeCircles?: number;
  }>(),
  {
    activeCircles: 8,
  },
);
</script>

<template>
  <div ref="loaderElement" class="relative opacity-100 w-100 h-100">
    <div
      v-for="i in 8"
      :key="i"
      class="circle absolute rounded-full h-10 w-10 transition-transform ease-in-out"
      :class="{
        'bg-white/25': activeCircles < i,
        'bg-white circle-active': activeCircles >= i,
      }"
      :style="`--circle-index: ${i - 1}`"
    ></div>
  </div>
</template>

<style scoped>
.circle {
  /* Paramètres du cercle */
  --circle-total: 8;
  --circle-radius: 160px;
  --circle-angle: calc(
    180deg + (var(--circle-index) * 360deg / var(--circle-total))
  );
  left: calc(50% + cos(var(--circle-angle)) * var(--circle-radius) - 1.2rem);
  top: calc(50% + sin(var(--circle-angle)) * var(--circle-radius) - 1.2rem);
}

.circle-active {
  /* Décalage directionnel lors de l'activation */
  transform: translate(
    calc(cos(var(--circle-angle)) * 2em),
    calc(sin(var(--circle-angle)) * 2em)
  );
}
</style>
