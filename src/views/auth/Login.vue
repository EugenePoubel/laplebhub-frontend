<script setup>
import axiosInstance from '@/lib/axios';
import { reactive } from 'vue';

const form = reactive ({
  email: '',
  password: '',
})

const errors = reactive({
  email: [],
  password: [],
});

const login = async (form) => {
    console.log("Logging ... ", form)
    await axiosInstance.get("/sanctum/csrf-cookie", {
      baseURL: "http://localhost:8000"
    });
    errors.email = [];
    errors.password = [];
    try {
        const response = await axiosInstance.post('/login', form);

    } catch (e) {
        if (e.response.status === 422) {
          errors.email = e.response.data.errors.email || [];
          errors.password = e.response.data.errors.password || [];
        }
    }
}
</script>

<template>
    <h1 class="text-3xl text-blue-600">Connexion</h1>

<form @submit.prevent="login(form)" class="max-w-sm mx-auto bg-white border border-gray-200 rounded-2xl shadow-xl p-8">
  <div class="mb-5">
    <label for="email" class="block mb-2.5 text-sm font-medium text-heading">Email</label>
    <input type="email" id="email" v-model="form.email" class="bg-neutral-secondary-medium border border-default-medium text-heading text-sm rounded-base focus:ring-brand focus:border-brand block w-full px-3 py-2.5 shadow-xs placeholder:text-body" placeholder="nom@protonmail.com" required />
      <span
        v-for="error in errors.email"
        :key="error"
        class="text-red-500 text-xs italic"
      >
        {{ error }}
      </span>
  </div>
  <div class="mb-5">
    <label for="password" class="block mb-2.5 text-sm font-medium text-heading">Mot de passe</label>
    <input type="password" id="password" v-model="form.password" class="bg-neutral-secondary-medium border border-default-medium text-heading text-sm rounded-base focus:ring-brand focus:border-brand block w-full px-3 py-2.5 shadow-xs placeholder:text-body" placeholder="••••••••" required />
      <span
        v-for="error in errors.password"
        :key="error"
        class="text-red-500 text-xs italic"
      >
        {{ error }}
      </span>
  </div>
  <button type="submit" class="text-white bg-brand box-border border border-transparent hover:bg-brand-strong focus:ring-4 focus:ring-brand-medium shadow-xs font-medium leading-5 rounded-base text-sm px-4 py-2.5 focus:outline-none">Se connecter</button>
</form>

</template>