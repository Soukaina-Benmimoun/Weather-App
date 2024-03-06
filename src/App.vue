<script setup>
import Search from './components/Search.vue';
import Weather from './components/Weather.vue';

import {ref} from 'vue';
const villes=ref([]);
const addVille = (data)=>{
  villes.value.push(data);

}
const deleteVille = (name) => {
  if (confirm('Are you sure')) {
    villes.value = villes.value.filter((p) => p.location.name !== name)
  }
}
</script>
<template>
  <div>
    <div class="text-center mb-6">
      {{ 
        new Date().toLocaleDateString('en-us',{
          year: 'numeric',
          month: 'long',
          day: 'numeric',
          weekday: 'long'
        })
        }}
    </div>
    <div class="text-center">
      <Search @ville-data="addVille" />
    </div>
    <div class="" style="display: flex; justify-content: space-around;">
      <div v-for="(ville, idx) in villes" :key="idx" style="padding: 5px;">
        <Weather :ville="ville" @delete-ville="deleteVille" />
      </div>
    </div>
 
  </div>
</template>