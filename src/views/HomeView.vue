<template>
  <div class="m-4 p-8 relative">
    <div aria-hidden="true" class="absolute -z-10 inset-0 grid grid-cols-2 -space-x-52 opacity-80">
        <div class="blur-[100px] h-56 bg-gradient-to-br from-primary to-purple-400 dark:from-blue-700"></div>
        <div class="blur-[100px] h-32 bg-gradient-to-r from-cyan-400 to-sky-300 dark:to-indigo-600"></div>
    </div>
    <div class="container flex flex-col items-center gap-8">
      <h1 class="text-7xl font-bold">Classic games written in Vue 3</h1>
      <div class="flex gap-4">
        <RouterLink v-for="link in links" :key="link" class="px-6 py-1.5 border border-white/50 rounded-md shadow-md bg-white/50 text-sm font-medium hover:-translate-y-0.5 transition-all duration-300" :to="{name: link.name}">{{ link.title }}</RouterLink>
      </div>
    </div>
  </div>
</template>

<script setup>
const links = [
  {
    name: 'tic-tac-toe',
    title: 'Tic Tac Toe'
  },
  {
    name: 'dice',
    title: 'Dice'
  },
]
</script>