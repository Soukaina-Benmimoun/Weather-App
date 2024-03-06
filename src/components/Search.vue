<script setup>
import { reactive } from 'vue';

const emit = defineEmits(['ville-data']);
const searchTerm = reactive({
  query: '',
  timeout: null,
  results: null,
})
const handleSearch = () => {
  clearTimeout(searchTerm.timeout)
  searchTerm.timeout = setTimeout(async () => {
    if (searchTerm.query !== '') {
      const res = await fetch(`http://api.weatherapi.com/v1/search.json?key=acd852848e8a4cdebe6111630240503&q=${searchTerm.query}`)
      const data = await res.json();
      searchTerm.results = data
    } else {
      searchTerm.results = null
    }

  }, searchTerm);
}
const getWeather = async (id) => {
  
  const res = await fetch(`http://api.weatherapi.com/v1/forecast.json?key=${YOUR_API_KEY}=&q=id:${id}&days=3&aqi=no&alerts=no`)
  const data = await res.json();

  emit('ville-data', data)
  searchTerm.query = '';
  searchTerm.results = null;
}



</script>

<template>
  <div>
    <!-- search field -->
    <form>
      <div class="bg-black border border-indigo-600/30 rounded-lg shadow-lg flex items-center">
        <i class="fa-solid fa-magnifying-glass p-2 text-indigo-600"></i>
        <input type="text" placeholder="Search for a ville"
          class="rounded-r-lg p-2 bg-black border-0 outline-0 focus:ring-2 focus:ring-indigo-600 ring-inset w-full"
          v-model="searchTerm.query" @input="handleSearch" />
      </div>
    </form>
    <!-- search suggestions -->
    <div class="bg-black my-2 rounded-lg shadow-lg">
      <div v-if="searchTerm.results !== null">
        <div v-for="ville in searchTerm.results" :key="ville.id">
          <button @click="getWeather(ville.id)"
            class="px-3 my-2 hover:text-indigo-600 hover:font-bold w-full text-left">
            {{ ville.name }},  {{ ville.country }}
          </button>
        </div>
      </div>
    </div>
  </div>
</template>