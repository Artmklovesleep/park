<template>
<section id="attractions" class="w-full py-12 md:py-24 lg:py-32 bg-muted">
    <div class="w-full mx-auto px-4 sm:px-6 lg:px-8">
      <div class="flex flex-col items-center justify-center space-y-4 text-center">
        <div class="space-y-2">
          <h2 class="text-3xl font-bold tracking-tighter sm:text-5xl">Наши аттракционы</h2>
          <p class="max-w-[900px] text-muted-foreground md:text-xl/relaxed lg:text-base/relaxed xl:text-xl/relaxed">    
От захватывающих природных чудес до захватывающих приключений, наша подобранная коллекция лучших достопримечательностей предлагает что-то для каждого.
          </p>
        </div>
      </div>
      <div class="mx-auto grid grid-cols-1 gap-6 py-12 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4">
        <div v-for="attraction in Attractions" :key="attraction.attractionId" class="group">
          <img
          :src="`${attraction.nameAttraction}.jpg`"
            width="300"
            height="300"
            :alt="attraction.nameAttraction"
            class="mx-auto aspect-square overflow-hidden rounded-xl object-cover object-center transition-all group-hover:scale-105"
          />
          <div class="mt-4 space-y-1">
            <h3 class="text-lg font-bold">{{ attraction.nameAttraction }}</h3>
            <p class="text-muted-foreground">{{ attraction.description }}</p>
          </div>
        </div>
      </div>
    </div>
  </section>
  </template>

<script setup>
definePageMeta({
    layout: "admin",
    middleware: "auth",
});

import { ref } from 'vue';
import { API } from '~/plugins/axios.js';

const Attractions = ref({ results: [] });

get_Attractions_data();

function get_Attractions_data() {
  API.get('Attractions')
    .then(response => {
      Attractions.value = response.data;
      console.log(Attractions.value);
    })
    .catch(error => {
      console.error('Ошибка при выполнении запроса:', error);
    });
}


useHead({ title: "Home" });

const { logout } = actions();
</script>
