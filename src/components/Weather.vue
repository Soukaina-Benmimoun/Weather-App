<script setup>
import { ref } from 'vue'


defineProps({
  ville: Object
})

const emit = defineEmits(['delete-ville'])

const removeVille = (villeName) => {
  emit('delete-ville', villeName)
}
</script>

<template>
  <div
    :class="ville.current.is_day === 1 ? 'bg-day' : 'bg-night'"
    class="text-white p-10 rounded-lg shadow-lg gap-6 mb-6 relative overflow-hidden"
  >
    <div class="mb-2 flex justify-between items-center">
      <div class="flex items-center justify-center gap-2">
        <h1 class="text-3xl">{{ ville.location.name }}</h1>
      </div>
      <div class="flex items-end justify-right gap-2">
        <h1 class="text-2xl">
          {{ new Date(ville.location.localtime).getHours() }}:{{
            new Date(ville.location.localtime).getMinutes()
          }}
        </h1>
      </div>
    </div>

    <div class="text-center flex-1">
      <img :src="ville.current.condition.icon" alt="icon" width="80" class="mx-auto -mb-10" style="margin-bottom: 5px;"/>
      <h1 class="text-8xl mb-2 -mr-4">{{ Math.round(ville.current.temp_c) }}&deg;</h1>
      <p class="text-2xl">{{ ville.current.condition.text }}</p>
    </div>

   
 

 
  </div>
</template>

<style scoped>
.bg-day {
  background-color: #8ec5fc;
  background-image: linear-gradient(62deg, #8ec5fc 0%, #efebf3 100%);
}
.bg-night {
  background-color: #07223d;
  background-image: linear-gradient(62deg, #0a2a4a 0%, #270845 100%);
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.2s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>