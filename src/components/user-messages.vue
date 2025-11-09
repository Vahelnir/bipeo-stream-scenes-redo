<script setup lang="ts">
import { onMounted, ref } from "vue";
import Modal from "./modal.vue";
import { faker } from "@faker-js/faker";
import { useIntervalFn } from "@vueuse/core";

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

function createMessage() {
  return {
    id: lastId.value++,
    username: faker.person.firstName(),
    content: faker.lorem.sentence(),
    position: {
      x: faker.number.int({ min: 0, max: 80 }),
      y: faker.number.int({ min: 0, max: 80 }),
    },
    duration: MESSAGE_DURATION,
  };
}

window.addMessage = () => {
  messages.value.push(createMessage());
};
</script>

<template>
  <div class="relative h-full w-full">
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
          top: message.position.y + '%',
          left: message.position.x + '%',
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
