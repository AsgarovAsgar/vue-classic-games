<script setup>
import { ref } from 'vue'
import ConfettiAnimation from '../components/ConfettiAnimation.vue';
const visible = ref(false)
const startAn = () => {
  visible.value = true
}
</script>

<template>
  <div class="about">
    <h1>This is an about page</h1>
    <button @click="startAn">Start</button>
    <ConfettiAnimation v-if="visible" />
  </div>
</template>
