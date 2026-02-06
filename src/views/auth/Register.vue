<script setup>
import axiosInstance from '@/lib/axios';
import { reactive } from 'vue';

const form = reactive ({
  name: '',
  email: '',
  password: '',
  password_confirmation: ''
})

const register = async (form) => {
    console.log("Registering ... ", form)
    await axiosInstance.get("/sanctum/csrf-cookie", {
      baseURL: "http://localhost:8000"
    });
    try {
        const response = await axiosInstance.post('/register', form);
        console.log(response.data);

    } catch (error) {
        console.error(error);
    }
}
</script>

<template>
    <h1 class="text-3xl text-blue-600">Inscription</h1>

<form @submit.prevent="register(form)" class="max-w-sm mx-auto bg-white border border-gray-200 rounded-2xl shadow-xl p-8">
  <div class="mb-5">
    <label for="username" class="block mb-2.5 text-sm font-medium text-heading">Nom d'utilisateur</label>
    <input v-model="form.name" type="text" id="username" class="bg-neutral-secondary-medium border border-default-medium text-heading text-sm rounded-base focus:ring-brand focus:border-brand block w-full px-3 py-2.5 shadow-xs placeholder:text-body" placeholder="nom d'utilisateur" required />
  </div>
  <div class="mb-5">
    <label for="email" class="block mb-2.5 text-sm font-medium text-heading">Email</label>
    <input type="email" id="email" v-model="form.email" class="bg-neutral-secondary-medium border border-default-medium text-heading text-sm rounded-base focus:ring-brand focus:border-brand block w-full px-3 py-2.5 shadow-xs placeholder:text-body" placeholder="nom@protonmail.com" required />
  </div>
  <div class="mb-5">
    <label for="password" class="block mb-2.5 text-sm font-medium text-heading">Mot de passe</label>
    <input type="password" id="password" v-model="form.password" class="bg-neutral-secondary-medium border border-default-medium text-heading text-sm rounded-base focus:ring-brand focus:border-brand block w-full px-3 py-2.5 shadow-xs placeholder:text-body" placeholder="••••••••" required />
  </div>
  <div class="mb-5">
    <label for="password_confirmation" class="block mb-2.5 text-sm font-medium text-heading">Confirmer le mot de passe</label>
    <input type="password" id="password_confirmation" v-model="form.password_confirmation" class="bg-neutral-secondary-medium border border-default-medium text-heading text-sm rounded-base focus:ring-brand focus:border-brand block w-full px-3 py-2.5 shadow-xs placeholder:text-body" placeholder="••••••••" required />
  </div>
  <button type="submit" class="text-white bg-brand box-border border border-transparent hover:bg-brand-strong focus:ring-4 focus:ring-brand-medium shadow-xs font-medium leading-5 rounded-base text-sm px-4 py-2.5 focus:outline-none">Créer un compte</button>
</form>


</template>