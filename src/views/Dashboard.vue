<script setup>
import axiosInstance from '@/lib/axios';
import { ref } from 'vue';

const user = ref ({
    name: "",
    email: ""
})

const getUser = async () => {
    try {
        const response = await axiosInstance.get('/user');
        user.value = response.data
    } catch (error) {
        console.error(error)
    }
};

const logout = async () => {
    try {
        await axiosInstance.post('/logout');
        user.value = {
             name: "",
             email: ""
        };
    } catch (error) {
        console.error(error);
    }
};

getUser();

</script>

<template>
    <h1 class="text-3xl text-blue-600">Tableau de bord</h1>
    <div class="flex items-center justify-between">
        <div class="block mb-2.5 text-sm font-medium text-heading">
            <p class="text-lg text-blue-500">Bienvenue, {{ user?.name }}</p>
            <p class="text-sm text-blue-500"> {{ user?.email }}</p>
        </div>

        <button @click="logout" class="text-white bg-brand box-border border border-transparent hover:bg-brand-strong focus:ring-4 focus:ring-brand-medium shadow-xs font-medium leading-5 rounded-base text-sm px-4 py-2.5 focus:outline-none">Se déconnecter</button>
    </div>
</template>