<script setup>
  import ConfettiExplosion from "vue-confetti-explosion";
</script>

<template>
  <div class="absolute left-1/2 h-screen transform -translate-x-1/2 -translate-y-1/2">
    <ConfettiExplosion :force="0.9" :duration="5000" :particleCount="200"/>
  </div>
</template>