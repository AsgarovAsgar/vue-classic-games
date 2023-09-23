<template>
  <div class="h-screen flex justify-center items-center w-full border p-4">
    <div class="border flex flex-col gap-2">
      <h1 class="font-semibold text-lg">Tic Tac Toe</h1>
      <p>{{ message }}</p>
      <div class="border grid grid-cols-3 gap-2 p-2">
        <div @click="addGo(index)" class="w-32 h-32 flex justify-center items-center border-2 cursor-pointer p-4" v-for="(cell, index) in startCells" :key="index">
          <p v-if="startCells[index] && cell === 'o'" class="rounded-full border-4 border-black w-16 h-16"></p>
          <p v-if="startCells[index] && cell === 'x'" class="">
            <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-20 h-20">
              <path stroke-linecap="round" stroke-linejoin="round" d="M6 18L18 6M6 6l12 12" />
            </svg>
          </p>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';
const startCells = ref(['', '', '', '', '', '', '', '', ''])
const activePlayer = ref('o')
const winnerPlayer = ref(null)
const winnerCombo = ref([])
const winnerCombos = [
  // Columns
  [0, 1, 2], [3, 4, 5], [6, 7, 8], 
  // Rows
  [0, 3, 6], [1, 4, 7], [2, 5, 8],  
  // Diagonals
  [0, 4, 8], [2, 4, 6]          
];

const message = ref('O starts first')

function addGo(index) {
  if(startCells.value[index] || winnerPlayer.value) return
  startCells.value[index] = activePlayer.value
  // check winner first and then switch player
  checkWinner()
  if(winnerPlayer.value) return
  activePlayer.value = activePlayer.value === 'o' ? 'x' : 'o'
  message.value = `It's now ${activePlayer.value.toUpperCase()}'s go`
}

function checkWinner() {
  winnerCombos.forEach(combo => {
    if(combo.every(cell => startCells.value[cell] === activePlayer.value)) {
      winnerPlayer.value = activePlayer.value
      message.value = `${winnerPlayer.value.toUpperCase()} wins!`
      winnerCombo.value = combo
      console.log('winnerCombo.value', winnerCombo.value);
    }
  })
}
</script>
