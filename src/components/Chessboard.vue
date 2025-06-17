<script setup lang="ts">
// Props
const props = defineProps<{
  ledger: LedgerEntry[];
}>();

export type LedgerEntry = { letter: string; num: number };

const letters = ["h", "g", "f", "e", "d", "c", "b", "a"];

const squares: LedgerEntry[] = [];
for (let num = 1; num <= 8; num++) {
  for (let c = 0; c < 8; c++) {
    squares.push({ letter: letters[c], num: num });
  }
}
</script>

<template>
  <!-- overflow-hidden is so rounded corners show -->
  <div class="aspect-square w-full rounded-xl overflow-hidden">
    <div class="grid grid-cols-8 grid-rows-8 w-full h-full">
      <span
        v-for="(square, index) in squares"
        :key="square.letter + square.num"
        :class="[
          'relative w-full h-full',
          // checkerboard color logic
          ledger.length &&
          square.num === ledger[ledger.length - 1].num &&
          square.letter === ledger[ledger.length - 1].letter
            ? 'bg-[#fcff5ecc]'
            : '',
          (square.num + index) % 2 === 0 ? 'bg-[#EBECD0]' : 'bg-[#739552]',
        ]"
        @click="$emit('updateLedger', square)"
      >
        <span v-if="square.letter === 'h'" class="absolute top-0 left-1">
          {{ square.num }}
        </span>
        <span v-if="square.num === 8" class="absolute bottom-0 right-1">
          {{ square.letter }}
        </span>
      </span>
    </div>
  </div>
</template>

<style scoped>
.read-the-docs {
  color: #888;
}
</style>
