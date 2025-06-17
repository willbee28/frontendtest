<script setup lang="ts">
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

<!-- <template>
 
  <div class="rounded-xl overflow-hidden">
    <div v-for="num in numbers" :key="num" class="grid grid-cols-8">
      <span
        v-for="(letter, index) in letters"
        :key="letter + num"
        :class="[
          'relative aspect-square',
          // checkerboard color logic
          (index + num) % 2 === 0 ? 'bg-[#EBECD0]' : 'bg-[#739552]',
        ]"
        @click="$emit('updateLedger', { letter, num })"
      >
        <span v-if="letter === 'a'" class="absolute top-0 left-1">{{
          num
        }}</span>
        <span v-if="num === 8" class="absolute bottom-0 right-1">{{
          letter
        }}</span>
      </span>
    </div>
  </div>
</template> -->

<!-- const letters = ["a", "b", "c", "d", "e", "f", "g", "h"];
const numbers = [1, 2, 3, 4, 5, 6, 7, 8];

const squares = [];
for (let r = 0; r < 8; r++) {
  for (let c = 0; c < 8; c++) {
    squares.push({ letter: letters[c], num: numbers[7 - r], row: r, col: c });
  }
}
</script>

<template>
  <div class="aspect-square w-full rounded-xl overflow-hidden">
    <div class="grid grid-cols-8 grid-rows-8 w-full h-full">
      <span
        v-for="square in squares"
        :key="square.letter + square.num"
        :class="[
          'relative w-full h-full',
          (square.row + square.col) % 2 === 0 ? 'bg-[#EBECD0]' : 'bg-[#739552]',
        ]"
        @click="$emit('updateLedger', square)"
      >
        <span v-if="square.letter === 'a'" class="absolute top-0 left-1">
          {{ square.num }}
        </span>
        <span v-if="square.num === 8" class="absolute bottom-0 right-1">
          {{ square.letter }}
        </span>
      </span>
    </div>
  </div>
</template> -->

<style scoped>
.read-the-docs {
  color: #888;
}
</style>
