<script setup lang="ts">
import { onMounted, ref } from "vue";
import { useIntervalFn } from "@vueuse/core";
import { faker } from "@faker-js/faker";

import Modal from "./modal.vue";

const MESSAGE_DURATION = 10; // in seconds

type Message = {
  id: number;
  username: string;
  content: string;
  position: {
    x: number;
    y: number;
  };
  duration: number;
};

const ALLOWED_SPAWN_AREAS = [
  { x: 1320, y: 50, width: 250, height: 800 },
  { x: 50, y: 50, width: 250, height: 800 },
  { x: 50, y: 50, width: 1500, height: 200 },
  { x: 50, y: 700, width: 1500, height: 150 },
];

const lastId = ref(0);
const messages = ref<Message[]>([]);

useIntervalFn(() => {
  // Remove messages that have expired
  messages.value = messages.value.filter((message) => message.duration > 0);

  for (const message of messages.value) {
    message.duration -= 1;
  }
}, 1000);

onMounted(() => {
  for (let i = 0; i < 5; i++) {
    messages.value.push(createMessage());
  }
});

function generatePosition() {
  let area;
  do {
    area =
      ALLOWED_SPAWN_AREAS[
        Math.floor(Math.random() * ALLOWED_SPAWN_AREAS.length)
      ];
  } while (!area);
  const x = Math.round(area.x + Math.random() * area.width);
  const y = Math.round(area.y + Math.random() * area.height);
  console.log(x, y);
  return { x, y };
}

function createMessage() {
  return {
    id: lastId.value++,
    username: faker.person.firstName(),
    content: faker.lorem.sentence(),
    position: generatePosition(),
    duration: MESSAGE_DURATION,
  };
}

// @ts-expect-error testing only
window.addMessage = () => {
  messages.value.push(createMessage());
};
</script>

<template>
  <div class="relative h-full w-full pointer-events-none">
    <TransitionGroup
      enter-active-class="transition-all duration-300 ease-in-out"
      enter-from-class="translate-y-5 scale-95 opacity-0"
      enter-to-class="translate-y-0 scale-100 opacity-100"
      leave-active-class="transition-all duration-300 ease-in-out"
      leave-from-class="translate-y-0 scale-100 opacity-100"
      leave-to-class="-translate-y-5 scale-95 opacity-0"
    >
      <Modal
        class="absolute h-30 w-80"
        :style="{
          top: message.position.y + 'px',
          left: message.position.x + 'px',
        }"
        v-for="message in messages"
        :key="message.id"
      >
        <template #header> &gt;_ {{ message.username }} </template>
        <p class="h-full w-full overflow-hidden wrap-break-word">
          {{ message.content }}
        </p>
        <template #progress>
          <div class="h-0.5 w-full">
            <div
              :style="{
                width: (message.duration / MESSAGE_DURATION) * 100 + '%',
              }"
              class="h-full bg-white transition-[width] duration-1000 ease-linear"
            ></div>
          </div>
        </template>
      </Modal>
    </TransitionGroup>
  </div>
</template>
