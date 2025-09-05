<script setup>
import { ref } from 'vue'
const contador = ref(0)
const increment = () => {
  contador.value++
}
const decrement = () => {
  contador.value--
}
</script>

<template>
  <section class="flex flex-col items-center gap-10">
    <h1 class="text-4xl">Contador vue</h1>
    <div class="flex items-center gap-10">
      <button class="text-xl border rounded-2xl px-4 py-2 hover:bg-white cursor-pointer" @click="increment">+</button>
      <p>{{ contador }}</p>
      <button class="text-xl border rounded-2xl px-4 py-2 hover:bg-white cursor-pointer" @click="decrement">-</button>
    </div>
    <div>
      <p>Olá</p>
    </div>
  </section>
</template>

<style scoped></style>
