<script setup>
import { ref } from 'vue'
import api from './plugins/api';

const username = ref('');
const password = ref('');
const error = ref('');
const isLoading = ref(false);
const ongs = ref();
const requestUrls = {
  token: '/token/',
  organizations: '/organizacoes/',

}
const login = async () => {
  isLoading.value = true
  error.value = ''

  try {
    const response = await api.post(requestUrls.token, {
      username: username.value,
      password: password.value
    })

    const { access, refresh } = response.data
    localStorage.setItem('accessToken', access)
    localStorage.setItem('refreshToken', refresh)

    console.log('Login bem sucedido')
    console.log(localStorage.getItem('accessToken'))
  } catch (err){
    error.value = 'Usuário ou senha inválidos'
    console.log(err)
  } finally {
    isLoading.value = false
    localStorage.clear()
  }
}
const getOngs = async () => {
  const data = await api.get(requestUrls.organizations, {
    headers: {
      Authorization: `Bearer ${localStorage.getItem('accessToken')}`
    }
  });
  ongs.value = data.data
}
</script>

<template>
   <h1 class="text-center ">
      Hello world!
  </h1>
  <form @submit.prevent="login">
    <input v-model="username" placeholder="Usuario" required class="border-1 border-cyan-200 rounded-2xl w-50 p-2 text-2xl bg-[url(bart.png)]">
    <input v-model="password" type="password" placeholder="Senha">
    <button type="submit" :disabled="isLoading">Entrar</button>
    <p v-if="error">{{ error }}</p>
    <button @click="getOngs" type="button">Carregar ongs</button>
    <p v-for="ong in ongs" :key="ong.id">
      {{ ong.nome }} 
    </p>
  </form>
</template>

<style scoped></style>
