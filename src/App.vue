<script setup lang="ts">
import { nextTick, onMounted, onBeforeUnmount, ref } from "vue";
import Chessboard, { type LedgerEntry } from "./components/Chessboard.vue";

const ledger = ref<LedgerEntry[]>([]);
const ledgerContainer = ref<HTMLElement | null>(null);
const windowHeight = ref(window.innerHeight);

const updateWindowHeight = () => {
  windowHeight.value = window.innerHeight;
};

onMounted(() => {
  window.addEventListener("resize", updateWindowHeight);
});

onBeforeUnmount(() => {
  window.removeEventListener("resize", updateWindowHeight);
});

const handleLedgerUpdate = (newLedgerEntry: LedgerEntry) => {
  ledger.value.push(newLedgerEntry);
  nextTick(() => {
    if (ledgerContainer.value) {
      ledgerContainer.value.scrollTop = ledgerContainer.value.scrollHeight;
    }
  });
};
</script>

<template>
  <div class="bg-[#393936] h-screen">
    <div
      class="text-white py-8 px-8 text-4xl w-1/2 mx-auto flex justify-center lg:justify-start"
    >
      Chess.com
    </div>
    <div class="xl:w-1/2 sm:w-3/5 mx-auto">
      <div
        class="flex flex-col lg:flex-row gap-4 m-4"
        :style="{ maxWidth: windowHeight + 'px' }"
      >
        <div class="flex flex-grow justify-center items-start">
          <Chessboard @updateLedger="handleLedgerUpdate" />
        </div>
        <div
          class="flex flex-col bg-[#2b2b2b] text-white rounded-lg p-4 lg:w-44 h-64 lg:h-auto overflow-y-auto custom-scrollbar"
          ref="ledgerContainer"
        >
          <div class="underline">Moves</div>
          <div v-for="(posit, index) in ledger" :key="posit.letter + posit.num">
            <span class="">
              {{ index }}. &nbsp;{{ posit.letter }}{{ posit.num }}
            </span>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
.custom-scrollbar {
  scrollbar-width: thin;
  scrollbar-color: rgba(255 255 255 / 0.29) transparent;
}
</style>
