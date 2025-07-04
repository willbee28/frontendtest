<script setup lang="ts">
import { nextTick, onMounted, onBeforeUnmount, ref } from "vue";
import Chessboard, { type LedgerEntry } from "./components/Chessboard.vue";
import Sidebar from "./components/Sidebar.vue";

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
    <div class="xl:w-1/2 md:w-3/5 w-auto mx-auto">
      <div
        class="text-white px-8 text-4xl w-1/2 lg:w-auto mx-auto flex justify-center lg:justify-start"
      >
        Chess.com
      </div>
      <div class="flex flex-col lg:flex-row gap-4 mx-4 justify-center">
        <div class="flex flex-row flex-grow justify-center lg:contents">
          <div
            class="flex-grow"
            :style="{ maxWidth: windowHeight - 50 + 'px' }"
          >
            <Chessboard @updateLedger="handleLedgerUpdate" :ledger="ledger" />
          </div>
        </div>
        <div
          class="flex flex-col bg-[#2b2b2b] text-white rounded-lg p-1 lg:mb-0 mb-4 lg:w-44 h-auto"
        >
          <Sidebar :ledger="ledger" :windowHeight="windowHeight" />
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
