<script setup>
import { ref, watch } from 'vue';

const props = defineProps({
  initialFilter: {
    type: String,
    default: ''
  }
});

const filterName = ref(props.initialFilter);
const emit = defineEmits(['filterChange']);

watch(filterName, (newFilter) => {
  emit('filterChange', newFilter);
});
</script>

<template>
   <div class="mb-6 flex justify-center py-6 bg-gradient-to-br from-red-900 to-black px-4 py-10 text-white">
    <div class="w-full max-w-md">
      <label for="movie-filter" class="block mb-3 text-lg font-semibold text-red-500 tracking-wide text-center">
        Filter by Title:
      </label>
      <div class="relative">
        <input
          id="movie-filter"
          v-model="filterName"
          type="text"
          placeholder="Search for a movie..."
          class="w-full px-4 py-2 rounded-md bg-black text-white placeholder-gray-500 focus:outline-none focus:ring-2 focus:ring-red-500 focus:ring-offset-2 focus:ring-offset-black shadow-sm"
        />
      </div>
    </div>
  </div>
</template>

