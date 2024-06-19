<template>
    <div class="flex flex-col min-h-[100dvh]">
      <header class="px-4 lg:px-6 h-14 flex items-center">
        <a class="flex items-center justify-center" href="#">
         
          <span class="sr-only">Аттракционы</span>
        </a>
        <nav class="ml-auto flex gap-4 sm:gap-6">
  <a class="text-sm font-medium hover:underline underline-offset-4" @click="scrollToSection('attractions')" href="#attractions">
    Аттракционы
  </a>
  <a class="text-sm font-medium hover:underline underline-offset-4" @click="scrollToSection('about')" href="#about">
    О нас
  </a>
  <a href="#contacts" class="text-sm font-medium hover:underline underline-offset-4" @click="scrollToSection('contacts')">
    Контакты
  </a>
</nav>

      </header>
      <main class="flex-1">
<section class="w-full mx-auto px-4 sm:px-6 lg:px-8 bg-white relative overflow-hidden h-screen">
    <div class="absolute inset-0 bg-center bg-cover"
         style="background-image: url('att.jpg'); filter: blur(3px);"></div>
    <div class="relative h-full flex items-center">
        <div class="mx-auto max-w-2xl text-center text-white px-4">
            <h1 class="text-3xl sm:text-5xl xl:text-6xl font-bold tracking-tighter mb-6">
                Откройте для себя лучшие аттракционы
            </h1>
            <p class="text-xl md:text-lg max-w-[600px] mx-auto mb-8">
                Исследуйте мир чудес и захватывающих приключений с нашей тщательно подобранной коллекцией лучших аттракционов. От захватывающих природных пейзажей до головокружительных приключений — у нас найдется что-то для каждого.
            </p>
            <div class="flex justify-center">
                <NuxtLink
                    to="register"
                    class="inline-flex items-center justify-center h-12 px-10 text-sm font-medium text-white bg-primary rounded-md shadow transition-colors hover:bg-primary/90 focus-visible:outline-none focus-visible:ring-1 focus-visible:ring-ring disabled:pointer-events-none disabled:opacity-50"
                >Исследовать Аттракционы</NuxtLink>
            </div>
        </div>
    </div>
</section>

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
  <section id="about" class="w-full py-12 md:py-24 lg:py-32 bg-muted">
  <div class="w-full mx-auto px-4 sm:px-6 lg:px-8">
    <div class="flex flex-col items-center justify-center space-y-4 text-center">
      <div class="space-y-2">
        <h2 class="text-3xl font-bold tracking-tighter sm:text-5xl">О нас</h2>
        <p class="max-w-[900px] text-muted-foreground md:text-xl/relaxed lg:text-base/relaxed xl:text-xl/relaxed">
          Добро пожаловать в парк развлечений "Мир Веселья" – место, где сбываются мечты и каждый найдет себе занятие по душе! Наш парк представляет собой уникальное сочетание захватывающих аттракционов, живописных зон отдыха и увлекательных шоу-программ.
          В нашем парке предусмотрено все для вашего комфорта: от просторных парковок и зон отдыха до удобных маршрутных схем и информационных киосков. Приезжайте в "Мир Веселья" с семьей и друзьями и подарите себе незабываемые моменты радости и веселья!
        </p>
      </div>
    </div>
  </div>
</section>

<section id="contacts" class="py-12 md:py-24 lg:py-32 bg-muted">
  <div class="mx-auto px-4 sm:px-6 lg:px-8">
    <div class="flex flex-col items-center justify-center space-y-4 text-center">
      <h2 class="text-3xl font-bold tracking-tighter sm:text-5xl">Контакты</h2>
      <p class="max-w-[900px] text-muted-foreground md:text-xl lg:text-base xl:text-xl">
        Наши контакты и социальные сети.
      </p>
    </div>
    <div class="grid grid-cols-1 gap-6 py-12 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4">
      <div class="group text-center">
        <a href="https://vk.com/" target="_blank">
          <img src="~/assets/img/vk.png" alt="Attraction" class="mx-auto rounded-xl object-cover object-center transition-all group-hover:scale-105" style="width: 150px; height: 150px;">
        </a>
        <div class="mt-4">
          <h3 class="text-lg font-bold">Вконтакте</h3>
        </div>
      </div>
      <div class="group text-center">
        <a href="https://web.telegram.org/" target="_blank">
          <img src="~/assets/img/telegram.png" alt="Attraction" class="mx-auto rounded-xl object-cover object-center transition-all group-hover:scale-105" style="width: 150px; height: 150px;">
        </a>
        <div class="mt-4">
          <h3 class="text-lg font-bold">Telegram</h3>
        </div>
      </div>
      <div class="group text-center">
        <a href="телефон" target="_blank">
          <img src="~/assets/img/phone-call.png" alt="Attraction" class="mx-auto rounded-xl object-cover object-center transition-all group-hover:scale-105" style="width: 150px; height: 150px;">
        </a>
        <div class="mt-4">
          <h3 class="text-lg font-bold">Номер телефона</h3>
        </div>
      </div>
      <div class="group text-center">
        <a href="https://web.whatsapp.com/" target="_blank">
          <img src="~/assets/img/whatsapp.png" alt="Attraction" class="mx-auto rounded-xl object-cover object-center transition-all group-hover:scale-105" style="width: 150px; height: 150px;">
        </a>
        <div class="mt-4">
          <h3 class="text-lg font-bold">Whatsapp</h3>
        </div>
      </div>
    </div>
  </div>
</section>



      </main>
      <footer class="flex flex-col gap-2 sm:flex-row py-6 w-full shrink-0 items-center px-4 md:px-6 border-t">
        <p class="text-xs text-muted-foreground">© 2024 Attractions. All rights reserved.</p>
        <nav class="sm:ml-auto flex gap-4 sm:gap-6"></nav>
      </footer>
    </div>
  </template>
  
  <script setup>
    import { API } from '~/plugins/axios.js';
    import { ref } from 'vue';
    import { onMounted } from 'vue';

  function scrollToSection(sectionId) {
    const section = document.getElementById(sectionId);
    if (section) {
      section.scrollIntoView({ behavior: 'smooth' });
    }
  }

  onMounted(() => {

    const hash = window.location.hash;
    if (hash) {
      const sectionId = hash.substring(1); 
      scrollToSection(sectionId);
    }
  });
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

  definePageMeta({
      middleware: "already-logged-in",
  });
  
  useHead({ title: "Welcome" });
  </script>
  
  <style></style>
  