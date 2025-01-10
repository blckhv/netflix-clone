<script setup>
import axios from 'axios';
import { onMounted, reactive } from 'vue';
import { useRoute, useRouter } from 'vue-router';
import { useToast } from 'vue-toastification';

const route = useRoute();
const router = useRouter();
const toast = useToast();

const movieId = route.params.id;

const formData = reactive({
  movie: {
    title: '',
    year: '',
    genre: '',
    rating: '',
    description: '',
    imageURL: ''
  }
});

const state = reactive({
  movie: {},
  isLoading: true
});

const handleSubmit = async () => {
  const updateMovie = {
    title: formData.movie.title,
    year: formData.movie.year,
    genre: formData.movie.genre,
    rating: formData.movie.rating,
    description: formData.movie.description,
    imageURL: formData.movie.imageURL
  }
  try {
    const response = await axios.put(`/api/movies/${movieId}`, updateMovie);
    toast.success('Movie updated successfully!');
    router.push(`/movies/${response.data.id}`);
  } catch (error) {
    console.error('Error updating movie:', error);
    toast.error('Movie was not updated!')
  }
};

onMounted(async () => {
  try {
    const response = await axios.get(`/api/movies/${movieId}`);
    state.movie = response.data;
    // Populate inputs
    formData.movie.title = state.movie.title;
    formData.movie.year = state.movie.year;
    formData.movie.genre = state.movie.genre;
    formData.movie.rating = state.movie.rating;
    formData.movie.description = state.movie.description;
    formData.movie.imageURL = state.movie.imageURL;
  } catch (error) {
    console.error('Error fetching movie', error);
  }
  finally {
    state.isLoading = false;
  }
});

</script>

<template>
  <div class="min-h-screen bg-gradient-to-br from-gray-900 via-gray-800 to-black text-white flex items-center justify-center p-6">
    <div class="bg-gray-800 p-8 rounded-lg shadow-2xl w-full max-w-3xl">
      <h1 class="text-3xl font-bold mb-6 text-center">Edit Movie</h1>

      <form @submit.prevent="handleSubmit" class="space-y-4">
        <div>
          <label for="title" class="block text-lg font-semibold">Title</label>
          <input
            id="title"
            v-model="formData.movie.title"
            type="text"
            class="w-full px-4 py-2 bg-gray-700 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500"
            required
          />
        </div>

        <div>
          <label for="year" class="block text-lg font-semibold">Year</label>
          <input
            id="year"
            v-model="formData.movie.year"
            type="number"
            min="1900"
            max="2025"
            class="w-full px-4 py-2 bg-gray-700 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500"
            required
          />
        </div>

        <div>
          <label for="genre" class="block text-lg font-semibold">Genre</label>
          <select
              id="genre"
              v-model="formData.movie.genre"
              class="w-full px-4 py-2 bg-gray-700 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500"
              required
            >
              <option value="Action">Action</option>
              <option value="Comedy">Comedy</option>
              <option value="Drama">Drama</option>
              <option value="Horror">Horror</option>
              <option value="Sci-Fi">Sci-Fi</option>
              <option value="Fantasy">Fantasy</option>
              <option value="Romance">Romance</option>
              <option value="Documentary">Documentary</option>
              <option value="Animation">Animation</option>
            </select>
        </div>

        <div>
          <label for="rating" class="block text-lg font-semibold">Rating</label>
          <input
            id="rating"
            v-model="formData.movie.rating"
            type="number"
            step="0.1"
            max="5"
            min="1"
            class="w-full px-4 py-2 bg-gray-700 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500"
            required
          />
        </div>

        <div>
          <label for="description" class="block text-lg font-semibold">Description</label>
          <textarea
            id="description"
            v-model="formData.movie.description"
            rows="4"
            class="w-full px-4 py-2 bg-gray-700 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500"
          ></textarea>
        </div>

        <div>
          <label for="imageURL" class="block text-lg font-semibold">Image URL</label>
          <input
            id="imageURL"
            v-model="formData.movie.imageURL"
            type="url"
            class="w-full px-4 py-2 bg-gray-700 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500"
            required
          />
        </div>

        <div class="flex justify-end mt-6 space-x-4">
          <button
            type="button"
            class="px-6 py-2 bg-gray-600 text-white rounded-lg hover:bg-gray-700 focus:ring-2 focus:ring-gray-500"
            @click="router.back()"
          >
            Cancel
          </button>
          <button
            type="submit"
            class="px-6 py-2 bg-blue-600 text-white rounded-lg hover:bg-blue-700 focus:ring-2 focus:ring-blue-500"
          >
            Save Changes
          </button>
        </div>
      </form>
    </div>
  </div>
</template>

<style scoped>
body {
  margin: 0;
}
</style>
