<script setup lang="ts">
import { ref } from "vue";
import { useAnimate } from "@vueuse/core";

import DashBorderOverlay from "../components/dash-border-overlay.vue";

const CIRCLE_START_ANGLE = 180;

const loaderElement = ref<HTMLElement | undefined>();
useAnimate(
  loaderElement,
  [
    { opacity: 0, transform: "translateX(-112.7%)" },
    { opacity: 0, transform: "translateX(-112.7%)", offset: 0.5 },
    { opacity: 1, transform: "translateX(-112.7%)", offset: 0.6 },
    { opacity: 1, transform: "translateX(-112.7%)", offset: 0.9 },
    { opacity: 1, transform: "translateX(0%)" },
  ],
  { duration: 3000, easing: "ease-in-out" },
);

function circleStyle(index: number, total: number, radius: number) {
  const angle = CIRCLE_START_ANGLE + ((index - 1) * 360) / total;
  const rad = (angle * Math.PI) / 180;
  const x = Math.cos(rad) * radius;
  const y = Math.sin(rad) * radius;
  return {
    left: `calc(50% + ${x}px - 1.2rem)`,
    top: `calc(50% + ${y}px - 1.2rem)`,
  };
}
</script>

<template>
  <DashBorderOverlay class="grid grid-cols-2">
    <div class="text-white font-bold overflow-hidden">
      <div>
        <div class="mb-8">
          <p class="text-[#030636] bg-white p-1 px-6 rounded text-lg">
            CopypeOS [v1.5.8] - Compilation personnalisée du noyau:
            xnu-bp/RELEASE_x64
          </p>
          <ul class="ps-6 mt-2">
            <li>Identifiant machine : BPE-LX9007-42</li>
            <li>Micrologiciel : EFI unifié Copypeo v3.2</li>
            <li>Démarrage sécurisé : ACTIVÉ</li>
          </ul>
        </div>

        <div class="mb-8">
          <p>[DÉMARRAGE] Vérification des interfaces matérielles...</p>
          <ul class="ps-6 mt-2">
            <li class="flex">
              <span class="flex-1">
                Processeur : Bipeon Zeta-9 @ 4.2THz (16 cœurs hybrides)
              </span>
              <span>[ OK ]</span>
            </li>
            <li class="flex">
              <span class="flex-1"> Mémoire : 65536Mo Q-RAM5 @ 10.4GT/s </span>
              <span>[ OK ]</span>
            </li>
            <li class="flex">
              <span class="flex-1">
                Carte graphique : NeuraX G1 Neural Array (1024 cours)
              </span>
              <span>[ OK ]</span>
            </li>
            <li class="flex">
              <span class="flex-1">
                Disque : Module FluxDrive NX1 2.5Po à état solide
              </span>
              <span>[ OK ]</span>
            </li>
            <li class="flex">
              <span class="flex-1"> TPM : Quantum Seal intégré v2.1 </span>
              <span>[ OK ]</span>
            </li>
            <li class="flex">
              <span class="flex-1">
                Refroidissement : Contrôleur ThermoSys v3.0
              </span>
              <span>[ OK ]</span>
            </li>
            <li class="flex">
              <span class="flex-1">
                Affichage : Interface VantaPanel UHDR (pipeline 64 bits)
              </span>
              <span>[ OK ]</span>
            </li>
            <li class="flex">
              <span class="flex-1"> Batterie : 87% - Santé optimale </span>
              <span>[ OK ]</span>
            </li>
          </ul>
        </div>

        <div class="mb-8">
          <p>[SÉCURITÉ]</p>
          <ul class="ps-6 mt-2">
            <li class="flex">
              <span class="flex-1"> Vérification du démarrage sécurisé </span>
              <span>[ OK ]</span>
            </li>
            <li class="flex">
              <span class="flex-1">
                Vérification des partitions protégées
              </span>
              <span>[ OK ]</span>
            </li>
            <li class="flex">
              <span class="flex-1"> Analyse des maliciels </span>
              <span>[ OK ]</span>
            </li>
            <li class="flex">
              <span class="flex-1"> Vérification des erreurs mémoire </span>
              <span>[ OK ]</span>
            </li>
            <li class="flex">
              <span class="flex-1">
                Intégrité système : empreinte SHA-256 validée
              </span>
              <span>[ OK ]</span>
            </li>
          </ul>
        </div>

        <div class="mb-8">
          <p>[INIT] Montage des systèmes de fichiers...</p>
          <ul class="ps-6 mt-2">
            <li class="flex">
              <span class="flex-1"> /dev/bpeOs1 monté sur / </span>
              <span>[ OK ]</span>
            </li>
            <li class="flex">
              <span class="flex-1"> /dev/bpeOs2 monté sur /home </span>
              <span>[ OK ]</span>
            </li>
            <li class="flex">
              <span class="flex-1"> /dev/bpeOs3 monté sur /data </span>
              <span>[ OK ]</span>
            </li>
          </ul>
        </div>

        <div class="mb-8">
          <p>[RÉSEAU] Initialisation de la pile réseau...</p>
          <ul class="ps-6 mt-2">
            <li class="flex">
              <span class="flex-1"> Interface wlano (Wi-Fi) détectée </span>
              <span>[ OK ]</span>
            </li>
            <li class="flex">
              <span class="flex-1">
                Connexion établie avec le point d'accès : "BipeoNet"
              </span>
              <span>[ OK ]</span>
            </li>
            <li class="flex">
              <span class="flex-1"> Liaison avec Tour-S v2.6 établie </span>
              <span>[ OK ]</span>
            </li>
            <li class="flex">
              <span class="flex-1">
                Canal de transmission activé : Port 8825 &lt;--› Relais orbital
              </span>
              <span>[ OK ]</span>
            </li>
            <li class="flex">
              <span class="flex-1"> Bail DHCP obtenu : 192.168.1.42 </span>
              <span>[ OK ]</span>
            </li>
            <li class="flex">
              <span class="flex-1"> Passerelle atteignable via Tour-S </span>
              <span>[ OK ]</span>
            </li>
            <li class="flex">
              <span class="flex-1"> Service DNS démarré (bpdnsd) </span>
              <span>[ OK ]</span>
            </li>
          </ul>
        </div>

        <div class="mb-8">
          <p>[SYSTÈME] Lancement des services de base...</p>
          <ul class="ps-6 mt-2">
            <li class="flex">
              <span class="flex-1"> Planificateur de tâches (bpe-crond) </span>
              <span>[ OK ]</span>
            </li>
            <li class="flex">
              <span class="flex-1"> Journalisation système (bpe-logger) </span>
              <span>[ OK ]</span>
            </li>
            <li class="flex">
              <span class="flex-1"> Service d'authentification (authd) </span>
              <span>[ OK ]</span>
            </li>
            <li class="flex">
              <span class="flex-1"> Démon de file de messages (mq-bpe) </span>
              <span>[ OK ]</span>
            </li>
            <li class="flex">
              <span class="flex-1">
                Observateur d'événements disque (fswatch)
              </span>
              <span>[ OK ]</span>
            </li>
          </ul>
        </div>

        <div class="mb-8">
          <p>[NŒUD CENTRAL] Démarrage des modules principaux...</p>
          <ul class="ps-6 mt-2">
            <li class="flex">
              <span class="flex-1"> MindCore v2.4.9 initialisé </span>
              <span>[ OK ]</span>
            </li>
            <li class="flex">
              <span class="flex-1"> Interface StreamBridge activée </span>
              <span>[ OK ]</span>
            </li>
            <li class="flex">
              <span class="flex-1">
                Démon de synchronisation audio/vidéo (avsd) lancé
              </span>
              <span>[ OK ]</span>
            </li>
            <li class="flex">
              <span class="flex-1"> Gestionnaire de scènes actif </span>
              <span>[ OK ]</span>
            </li>
            <li class="flex">
              <span class="flex-1"> Pipeline de rendu Overlay prêt </span>
              <span>[ OK ]</span>
            </li>
            <li class="flex">
              <span class="flex-1"> AudioMux : 2 canaux détectés </span>
              <span>[ OK ]</span>
            </li>
            <li class="flex">
              <span class="flex-1">
                Nœud encodeur (x264 / AAC) opérationnel
              </span>
              <span>[ OK ]</span>
            </li>
            <li class="flex">
              <span class="flex-1"> Collecteur de métriques en service </span>
              <span>[ OK ]</span>
            </li>
          </ul>
        </div>

        <div class="mb-8">
          <p class="text-[#030636] bg-white p-1 px-6 rounded text-lg">
            Liste des viewers ayant envoyé un message dans le chat :
          </p>
          <ul class="ps-20 mt-2">
            <li class="flex">
              <span class="flex-1"> - A </span>
              <span>[ 77 MSG ]</span>
            </li>
          </ul>
        </div>

        <div class="mb-6">
          <p class="text-[#030636] bg-white p-1 px-6 rounded text-lg">
            Démarrage terminé. Lancement immédiat de l'interface graphique...
          </p>
        </div>
      </div>
    </div>

    <div class="flex justify-center items-center">
      <div ref="loaderElement" class="relative opacity-100 w-100 h-100">
        <div
          v-for="i in 8"
          :key="i"
          class="absolute bg-white/25 rounded-full h-10 w-10"
          :style="circleStyle(i, 8, 10 * 16)"
        ></div>
      </div>
    </div>
  </DashBorderOverlay>
</template>
