<script setup lang="ts">
import type { LedgerEntry } from "./Chessboard.vue";

// Props
const props = defineProps<{
  ledger: LedgerEntry[];
  windowHeight: number;
}>();
</script>

<template>
  <div class="underline mb-2">Moves</div>
  <div
    class="bg-[#454545] p-2 rounded-sm h-24 lg:h-64 overflow-y-auto custom-scrollbar"
    ref="ledgerContainer"
    :style="{ maxHeight: props.windowHeight - 100 + 'px' }"
  >
    <div
      v-for="(posit, index) in props.ledger"
      :key="posit.letter + posit.num"
      class="inline-block lg:flex"
    >
      <span>
        {{ index }}. &nbsp;{{ posit.letter }}{{ posit.num }} &nbsp; &nbsp;
      </span>
    </div>
  </div>
</template>

<style scoped></style>
