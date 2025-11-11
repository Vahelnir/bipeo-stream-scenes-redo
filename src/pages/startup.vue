<script setup lang="ts">
import { computed, onMounted, reactive, ref } from "vue";
import { useCurrentElement } from "@vueuse/core";
import { faker } from "@faker-js/faker";
import { useRouter } from "vue-router";

import DashBorderOverlay from "../components/dash-border-overlay.vue";
import { roundDecimals } from "../utils/round-decimals";
import { wait } from "../utils/wait";

const CIRCLE_START_ANGLE = 180;

const router = useRouter();

const componentRootElement = useCurrentElement<HTMLElement>();
const loaderElement = ref<HTMLElement | undefined>();

function circleStyle(index: number, total: number, radius: number) {
  const angle = CIRCLE_START_ANGLE + ((index - 1) * 360) / total;
  const rad = (angle * Math.PI) / 180;
  const cosX = roundDecimals(Math.cos(rad), 2);
  const sinY = roundDecimals(Math.sin(rad), 2);
  const x = cosX * radius;
  const y = sinY * radius;
  return {
    left: `calc(50% + ${x}px - 1.2rem)`,
    top: `calc(50% + ${y}px - 1.2rem)`,
    "--circle-translate-x": cosX,
    "--circle-translate-y": sinY,
  };
}

type Block = {
  type: "category" | "sub-category";
  title: string;
  logs: {
    label: string;
    status?: string;
    after?: number;
  }[];
  after?: number;
  bigPadding: boolean;
};

const logs: Block[] = [
  {
    type: "category",
    after: 1000,
    title:
      "CopypeOS [v1.5.8] - Compilation personnalisée du noyau: xnu-bp/RELEASE_x64",
    logs: [
      { label: "Identifiant machine : BPE-LX9007-42", after: 100 },
      { label: "Micrologiciel : EFI unifié Copypeo v3.2", after: 100 },
      { label: "Démarrage sécurisé : ACTIVÉ", after: 100 },
    ],
    bigPadding: false,
  },
  {
    type: "sub-category",
    title: "[DÉMARRAGE] Vérification des interfaces matérielles...",
    logs: [
      {
        after: 1000,
        label: "Processeur : Bipeon Zeta-9 @ 4.2THz (16 cœurs hybrides)",
        status: "OK",
      },
      {
        after: 100,
        label: "Mémoire : 65536Mo Q-RAM5 @ 10.4GT/s",
        status: "OK",
      },
      {
        after: 100,
        label: "Carte graphique : NeuraX G1 Neural Array (1024 cours)",
        status: "OK",
      },
      {
        after: 700,
        label: "Disque : Module FluxDrive NX1 2.5Po à état solide",
        status: "OK",
      },
      {
        after: 100,
        label: "TPM : Quantum Seal intégré v2.1",
        status: "OK",
      },
      {
        after: 100,
        label: "Refroidissement : Contrôleur ThermoSys v3.0",
        status: "OK",
      },
      {
        after: 100,
        label: "Affichage : Interface VantaPanel UHDR (pipeline 64 bits)",
        status: "OK",
      },
      {
        after: 100,
        label: "Batterie : 87% - Santé optimale",
        status: "OK",
      },
    ],
    bigPadding: false,
  },
  {
    type: "sub-category",
    title: "[SÉCURITÉ]",
    after: 1000,
    logs: [
      {
        after: 100,
        label: "Vérification du démarrage sécurisé",
        status: "OK",
      },
      {
        after: 100,
        label: "Vérification des partitions protégées",
        status: "OK",
      },
      {
        after: 100,
        label: "Analyse des maliciels",
        status: "OK",
      },
      {
        label: "Vérification des erreurs mémoire",
        status: "OK",
      },
      {
        after: 100,
        label: "Intégrité système : empreinte SHA-256 validée",
        status: "OK",
      },
    ],
    bigPadding: false,
  },
  {
    type: "sub-category",
    title: "[INIT] Montage des systèmes de fichiers...",
    after: 100,
    logs: [
      {
        after: 500,
        label: "/dev/bpeOs1 monté sur /",
        status: "OK",
      },
      {
        after: 100,
        label: "/dev/bpeOs2 monté sur /home",
        status: "OK",
      },
      {
        after: 100,
        label: "/dev/bpeOs3 monté sur /data",
        status: "OK",
      },
    ],
    bigPadding: false,
  },
  {
    type: "sub-category",
    title: "[RÉSEAU] Initialisation de la pile réseau...",
    logs: [
      {
        after: 500,
        label: "Interface wlano (Wi-Fi) détectée",
        status: "OK",
      },
      {
        after: 100,
        label: "Connexion établie avec le point d'accès : 'BipeoNet'",
        status: "OK",
      },
      {
        after: 100,
        label: "Liaison avec Tour-S v2.6 établie",
        status: "OK",
      },
      {
        after: 100,
        label: "Canal de transmission activé : Port 8825 <--> Relais orbital",
        status: "OK",
      },
      {
        after: 100,
        label: "Bail DHCP obtenu : 192.168.1.42",
        status: "OK",
      },
      {
        after: 100,
        label: "Passerelle atteignable via Tour-S",
        status: "OK",
      },
      {
        after: 500,
        label: "Service DNS démarré (bpdnsd)",
        status: "OK",
      },
    ],
    bigPadding: false,
  },
  {
    type: "sub-category",
    after: 500,
    title: "[SYSTÈME] Lancement des services de base...",
    logs: [
      {
        after: 100,
        label: "Planificateur de tâches (bpe-crond)",
        status: "OK",
      },
      {
        after: 100,
        label: "Journalisation système (bpe-logger)",
        status: "OK",
      },
      {
        after: 100,
        label: "Service d'authentification (authd)",
        status: "OK",
      },
      {
        after: 100,
        label: "Démon de file de messages (mq-bpe)",
        status: "OK",
      },
      {
        after: 100,
        label: "Observateur d'événements disque (fswatch)",
        status: "OK",
      },
    ],
    bigPadding: false,
  },
  {
    type: "sub-category",
    after: 100,
    title: "[NŒUD CENTRAL] Démarrage des modules principaux...",
    logs: [
      {
        after: 500,
        label: "MindCore v2.4.9 initialisé",
        status: "OK",
      },
      {
        after: 100,
        label: "Interface StreamBridge activée",
        status: "OK",
      },
      {
        after: 100,
        label: "Démon de synchronisation audio/vidéo (avsd) lancé",
        status: "OK",
      },
      {
        after: 100,
        label: "Gestionnaire de scènes actif",
        status: "OK",
      },
      {
        after: 100,
        label: "Pipeline de rendu Overlay prêt",
        status: "OK",
      },
      {
        after: 100,
        label: "AudioMux : 2 canaux détectés",
        status: "OK",
      },
      {
        after: 100,
        label: "Nœud encodeur (x264 / AAC) opérationnel",
        status: "OK",
      },
      {
        after: 100,
        label: "Collecteur de métriques en service",
        status: "OK",
      },
    ],
    bigPadding: false,
  },
  {
    type: "sub-category",
    after: 100,
    title: "[RÉSEAU] Connexion aux services de diffusion...",
    logs: [
      {
        after: 500,
        label: "Résolution de api.twitch.tv...",
        status: "OK",
      },
      {
        after: 100,
        label: "Connexion établie avec le serveur d'ingest Twitch (par01)...",
        status: "OK",
      },
      {
        after: 100,
        label: "Clé de stream vérifiée",
        status: "OK",
      },
      {
        after: 100,
        label: "Démon d'écoute du chat initialisé",
        status: "OK",
      },
      {
        after: 500,
        label: "Lien virtuel OBSLink établi",
        status: "OK",
      },
      {
        after: 100,
        label: "Surveillance du temps de diffusion activée",
        status: "OK",
      },
      {
        after: 100,
        label: "WebSocket : chat.bipeo.lan <-> passerelle IRC Twitch en ligne",
        status: "OK",
      },
      {
        after: 100,
        label: "Analyse du stream...",
        status: "OK",
      },
    ],
    bigPadding: false,
  },
  // TODO: move this in the wholeAnimation function
  {
    type: "category",
    after: 400,
    title: "Liste des viewers ayant envoyé un message dans le chat :",
    logs: Array.from({ length: 12 }, (_, i) => ({
      after: 50,
      label: `- ${faker.internet.displayName()}`,
      messageCount: faker.number.int({ min: 1, max: 150 }),
      get status() {
        return `${this.messageCount} MSG`;
      },
    })).sort((a, b) => b.messageCount - a.messageCount),
    bigPadding: true,
  },
  {
    type: "category",
    title: "Démarrage terminé. Lancement immédiat de l'interface graphique...",
    logs: [],
    bigPadding: false,
  },
];

const visibleBlocks = ref<Block[]>([]);
const finishedStepsCount = computed(() =>
  Math.max(visibleBlocks.value.length - 1, 0),
);

onMounted(async () => {
  await wholeAnimation();
});

async function wholeAnimation() {
  await animateLoaderInPlace().finished;

  await animateLogsWriting();
  await wait(400);

  await animateBlinkLoaderSuccess().finished;
  await wait(1000);

  await componentRootElement.value.animate([{ opacity: 1 }, { opacity: 0 }], {
    duration: 500,
    fill: "forwards",
  }).finished;

  await nextPage();
}

function animateLoaderInPlace() {
  if (!loaderElement.value) {
    throw new Error("Loader element not found");
  }

  return loaderElement.value.animate(
    [
      { opacity: 0, transform: "translateX(-112.7%)" },
      { opacity: 0, transform: "translateX(-112.7%)", offset: 0.5 },
      { opacity: 1, transform: "translateX(-112.7%)", offset: 0.6 },
      { opacity: 1, transform: "translateX(-112.7%)", offset: 0.9 },
      { opacity: 1, transform: "translateX(0%)" },
    ],
    { duration: 3000, easing: "ease-in-out" },
  );
}

function animateBlinkLoaderSuccess() {
  if (!loaderElement.value) {
    throw new Error("Loader element not found");
  }

  return loaderElement.value.animate(
    [{ opacity: 1 }, { opacity: 0.25 }, { opacity: 1 }],
    { duration: 125, iterations: 2 },
  );
}

async function animateLogsWriting() {
  for (const block of logs) {
    const visibleBlock: Block = reactive({ ...block, logs: [] });
    if (block.after !== undefined && block.after > 0) {
      await wait(block.after);
    }
    visibleBlocks.value.push(visibleBlock);

    for (const log of block.logs) {
      if (log.after !== undefined && log.after > 0) {
        await wait(log.after);
      }
      visibleBlock.logs.push(log);
    }
  }
}

function nextPage() {
  return router.push({ name: "/loader" });
}
</script>

<template>
  <DashBorderOverlay class="grid grid-cols-2">
    <div class="flex flex-col text-white font-bold overflow-hidden justify-end">
      <div>
        <div v-for="(block, bIdx) in visibleBlocks" :key="bIdx" class="mb-6">
          <p
            v-if="block.title"
            :class="
              block.type === 'category'
                ? 'text-bipeo-dark-blue bg-white px-6 rounded text-lg'
                : ''
            "
          >
            {{ block.title }}
          </p>
          <ul :class="block.bigPadding ? 'ps-12 mt-2' : 'ps-6 mt-2'">
            <li v-for="(log, i) in block.logs" :key="i" class="flex">
              <span class="flex-1">{{ log.label }}</span>
              <span v-if="'status' in log">[ {{ log.status }} ]</span>
            </li>
          </ul>
        </div>
      </div>
    </div>

    <div class="flex justify-center items-center">
      <div ref="loaderElement" class="relative opacity-100 w-100 h-100">
        <div
          v-for="i in 8"
          :key="i"
          class="absolute rounded-full h-10 w-10 transition-transform ease-in-out"
          :class="{
            'bg-white/25': finishedStepsCount < i,
            'bg-white circle-active': finishedStepsCount >= i,
          }"
          :style="circleStyle(i, 8, 10 * 16)"
        ></div>
      </div>
    </div>
  </DashBorderOverlay>
</template>

<style scoped>
.circle-active {
  transform: translate(
    calc(var(--circle-translate-x) * 2em),
    calc(var(--circle-translate-y) * 2em)
  );
}
</style>
