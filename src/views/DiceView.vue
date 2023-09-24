<script setup>
import { ref } from 'vue'
import ConfettiAnimation from '@/components/ConfettiAnimation.vue';
const dice = ref(null)
const maxPoint = ref(100)
const playing = ref(true)
const player1Score = ref(0)
const player2Score = ref(0)
const currentScore = ref(0)

const activePlayer = ref(0)
const winnerPlayer = ref(null)

const rollDice = () => {
  if(!playing.value) return
  dice.value = Math.trunc(Math.random() * 6) + 1;
  if(dice.value === 1) {
    switchPlayer()
  } else {
    currentScore.value += dice.value
  }
}

const holdDice = () => {
  if(!playing.value) return
  activePlayer.value === 0 ? player1Score.value += currentScore.value : player2Score.value += currentScore.value

  if(player1Score.value >= maxPoint.value || player2Score.value >= maxPoint.value) {
    player1Score.value >= maxPoint.value ? winnerPlayer.value = 0 : winnerPlayer.value = 1
    playing.value = false
    dice.value = null
  } else {
    switchPlayer()
  }
}

const resetGame = () => {
  playing.value = true
  dice.value = winnerPlayer.value = null
  player1Score.value = player2Score.value = currentScore.value = activePlayer.value = 0
}

const switchPlayer = () => {
  currentScore.value = 0
  activePlayer.value = activePlayer.value === 0 ? 1 : 0
}

</script>

<template>
  <div class="relative">
  <div class="font-['Nunito'] text-[#333] h-screen flex justify-center items-center bg-gradient-to-tl from-[#753682] to-[#20901a]">
    <main class="relative flex w-[90%] h-[90%] bg-black/40 backdrop-blur-md shadow-lg rounded-xl overflow-hidden">
      <section
        class="w-1/2 flex flex-col items-center p-32 transition-all duration-100"
        :style="{backgroundColor: activePlayer === 0 ? 'rgb(255 255 255 / 0.6)' : 'rgb(255 255 255 / 0.4)' }"
      >
        <h2 class="relative text-6xl uppercase font-light" id="name--0">Player 1</h2>
        <p class="text-[8rem] text-[#c7365f] font-light">{{ player1Score }}</p>
        <div class="bg-[#c7365f] opacity-80 rounded-xl text-white p-8 text-center transition-all duration-100 w-[70%]">
          <p class="uppercase text-3xl text-[#ddd]">Current</p>
          <p class="text-[3.5rem]">{{ activePlayer === 0 ? currentScore : '0' }}</p>
        </div>
      </section>
      <section
        class="w-1/2 flex flex-col items-center p-32 transition-all duration-100 bg-white/30"
        :style="{backgroundColor: activePlayer === 1 ? 'rgb(255 255 255 / 0.6)' : 'rgb(255 255 255 / 0.4)' }"
      >
        <h2 class="relative text-6xl uppercase font-light" id="name--1">Player 2</h2>
        <p class="text-[8rem] text-[#c7365f] font-light" id="score--1">{{ player2Score }}</p>
        <div class="bg-[#c7365f] opacity-80 rounded-xl text-white p-8 text-center transition-all duration-100 w-[70%]">
          <p class="uppercase text-3xl text-[#ddd]">Current</p>
          <p class="text-[3.5rem]" id="current--1">{{ activePlayer === 1 ? currentScore : '0' }}</p>
        </div>
      </section>

      <div class="py-12 pb-20 flex flex-col justify-between absolute left-1/2 h-full transform -translate-x-1/2">
        <button @click="resetGame" class="text-[#444] bg-white/60 backdrop-blur-md py-3 px-14 shadow-md rounded-full text-2xl uppercase transition-all duration-100 active:translate-y-0.5 active:shadow-xl">🔄 New game</button>
        <img v-show="dice" :src="`/dice-nums/dice-${dice}.png`" alt="Playing dice" class="w-40 self-center shadow-lg" />
        <div v-if="!playing" class="translate-y-4 transition-all duration-100 uppercase rounded-lg shadow-lg py-6 p-4 backdrop-blur-md flex flex-col text-center gap-2 text-white text-3xl bg-white/20">
          <h3>Player {{ winnerPlayer + 1 }} won</h3>
          <p>Congrats 👏</p>
        </div>
        <div class="flex flex-col gap-6">
          <button @click="rollDice" class="text-[#444] bg-white/60 backdrop-blur-md py-3 px-14 shadow-md rounded-full text-2xl uppercase transition-all duration-100 active:translate-y-0.5 active:shadow-xl">🎲 Roll dice</button>
          <button @click="holdDice" class="text-[#444] bg-white/60 backdrop-blur-md py-3 px-14 shadow-md rounded-full text-2xl uppercase transition-all duration-100 active:translate-y-0.5 active:shadow-xl">📥 Hold</button>
        </div>
      </div>
    </main>
  </div>
  <ConfettiAnimation v-if="!playing" />
</div>
</template>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Nunito&display=swap');
</style>
