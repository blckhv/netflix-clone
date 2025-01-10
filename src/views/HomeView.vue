<script setup>
import MovieListings from '@/components/MovieListings.vue';
import { ref } from 'vue';

const movCount = ref(0);
const limitCount = ref(4);

const updateMovieCount = (movieCount) => {
  movCount.value = movieCount;
};
</script>

<template>
  <div class="py-10">
    <MovieListings @jsonLoaded="updateMovieCount" :limit="limitCount" :sortBy=" 'name' " showLoadMoreBtn="true" />
  </div>
</template>
