<script setup>
import Search from './components/Search.vue';
import {ref} from 'vue';
const villes=ref([]);
const addVille = (data)=>{
  villes.value.push(data);

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
    <div>
      <Search @ville-data="addVille" />
    </div>
    <div>
      <p v-for="ville in villes">{{ ville.location.name }},
      {{ ville.current.temp_c}} °C.  {{ ville.location.localtime }}
    </p>
    </div>
  </div>
</template>