<script setup>
import { RouterLink, RouterView } from 'vue-router'
</script>

<template>
  <div class="min-h-screen flex flex-col bg-gray-50 dark:bg-gray-900 text-gray-900 dark:text-gray-100 font-sans">
    
    <header class="sticky top-0 z-50 w-full border-b border-gray-200 bg-white/80 backdrop-blur-md dark:bg-gray-950/80 dark:border-gray-800">
      <nav class="mx-auto flex max-w-7xl items-center justify-between p-4 px-6">
        
        <RouterLink class="text-xl font-bold tracking-tight text-blue-600 dark:text-blue-500 hover:text-blue-700 transition-colors" to="/">
          LaPlebHub
        </RouterLink>
        
        <div class="flex items-center gap-4">
          <RouterLink class="text-sm font-medium text-gray-700 hover:text-blue-600 dark:text-gray-300 dark:hover:text-blue-400 transition-colors" to="/login">
            Se Connecter
          </RouterLink>
          
          <RouterLink class="rounded-lg bg-blue-700 px-4 py-2 text-sm font-medium text-white hover:bg-blue-800 focus:outline-none focus:ring-4 focus:ring-blue-300 dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800 transition-all" to="/register">
            Inscription
          </RouterLink>  
        </div>

      </nav>
    </header>

    <main class="flex-grow">
      <div class="mx-auto max-w-6xl px-4 py-8 sm:px-6 lg:px-8">
        <RouterView />
      </div>
    </main>
    
  </div>
</template>