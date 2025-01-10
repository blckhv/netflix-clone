<script setup>
  import logo from '@/components/icons/logo.png';
import { RouterLink, useRoute } from 'vue-router';

const isActiveLink = (routePath) => {
  const route = useRoute();
  return route.path === routePath;
}
</script>

<template>
    <nav class="bg-gradient-to-r from-red-900 to-black border-b border-red-500">
      <div class="mx-auto max-w-7xl px-2 sm:px-6 lg:px-8">
        <div class="flex h-20 items-center justify-between">
          <div
            class="flex flex-1 items-center justify-center md:items-stretch md:justify-start"
          >
            <!-- Logo -->
            <RouterLink class="flex flex-shrink-0 items-center mr-4" to="/">
              <img class="h-10 w-auto" :src="logo" alt="Vue Jobs" />
              <span class="hidden md:block text-red-500 text-2xl font-bold ml-2"
                >My Movies</span
              >
            </RouterLink>
            <div class="md:ml-auto">
              <div class="flex space-x-2">
                <RouterLink
                  to="/"
                  :class="[
                    isActiveLink('/') 
                    ? 'bg-red-700' 
                    : 'hover:bg-red-600 hover:text-red-300',
                    'text-white',
                    'px-3',
                    'py-2',
                    'rounded-md']"
                  >Home</RouterLink
                >
                <RouterLink
                  to="/movies"
                  :class="[
                    isActiveLink('/movies') 
                    ? 'bg-red-700' 
                    : 'hover:bg-red-600 hover:text-red-300',
                    'text-white',
                    'px-3',
                    'py-2',
                    'rounded-md']"
                  >Movies</RouterLink
                >
                <RouterLink
                  to="/movies/add"
                  :class="[
                    isActiveLink('/movies/add') 
                    ? 'bg-red-700' 
                    : 'hover:bg-red-600 hover:text-red-300',
                    'text-white',
                    'px-3',
                    'py-2',
                    'rounded-md']"
                  >Add Movie</RouterLink
                >
              </div>
            </div>
          </div>
        </div>
      </div>
    </nav>
</template>