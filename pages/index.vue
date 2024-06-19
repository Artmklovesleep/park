<template>
    <div class="flex flex-col min-h-[100dvh]">
      <header class="px-4 lg:px-6 h-14 flex items-center">
        <a class="flex items-center justify-center" href="#">
         
          <span class="sr-only">Attractions</span>
        </a>
        <nav class="ml-auto flex gap-4 sm:gap-6">
          <a class="text-sm font-medium hover:underline underline-offset-4" href="#">
            Attractions
          </a>
          <a class="text-sm font-medium hover:underline underline-offset-4" href="#">
            About
          </a>
          <a href="#" class="text-sm font-medium hover:underline underline-offset-4">
            Contact
          </a>
        </nav>
      </header>
      <main class="flex-1">
        <section class="w-full py-12 sm:py-24 lg:py-32 bg-cover bg-center" :style="{background-image:url(~/assets/img/att.jpg)}">
    <div class="w-full mx-auto px-4 sm:px-6 lg:px-8 bg-white bg-opacity-80">
        <div class="flex grid gap-6 lg:grid-cols-[1fr_550px] lg:gap-12 xl:grid-cols-[1fr_650px]">
            <div class="flex flex-col justify-center space-y-6">
                <div class="space-y-4">
                    <h1 class="text-3xl font-bold tracking-tighter sm:text-5xl xl:text-6xl/none text-white">
                        Откройте для себя лучшие аттракционы
                    </h1>
                    <p class="max-w-[600px] text-white md:text-xl">
                        Исследуйте мир чудес и захватывающих приключений с нашей тщательно подобранной коллекцией лучших аттракционов. От захватывающих природных пейзажей до головокружительных приключений — у нас найдется что-то для каждого.
                    </p>
                </div>
                <div class="flex flex-col gap-2 min-[400px]:flex-row">
                    <NuxtLink
                        to="register"
                        class="inline-flex h-12 items-center justify-center rounded-md bg-primary px-10 text-sm font-medium text-white shadow transition-colors hover:bg-primary/90 focus-visible:outline-none focus-visible:ring-1 focus-visible:ring-ring disabled:pointer-events-none disabled:opacity-50"
                    >Исследовать Аттракционы</NuxtLink>
                </div>
            </div>
        </div>
    </div>
</section>


        <section class="w-full py-12 md:py-24 lg:py-32 bg-muted">
            <div class="w-full mx-auto px-4 sm:px-6 lg:px-8">
            <div class="flex flex-col items-center justify-center space-y-4 text-center">
              <div class="space-y-2">
                <h2 class="text-3xl font-bold tracking-tighter sm:text-5xl">Explore Our Top Attractions</h2>
                <p class="max-w-[900px] text-muted-foreground md:text-xl/relaxed lg:text-base/relaxed xl:text-xl/relaxed">
                  From stunning natural wonders to thrilling adventures, our curated collection of top attractions
                  offers something for everyone.
                </p>
              </div>
            </div>
            <div class="mx-auto grid grid-cols-1 gap-6 py-12 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4">
              <div class="group">
                <img
                  src="~/assets/img/man.png"
                  width="300"
                  height="300"
                  alt="Attraction"
                  style=""
                  class="mx-auto aspect-square overflow-hidden rounded-xl object-cover object-center transition-all group-hover:scale-105"
                />
                <div class="mt-4 space-y-1">
                  <h3 class="text-lg font-bold">Grand Canyon</h3>
                  <p class="text-muted-foreground">Explore the breathtaking natural wonder of the Grand Canyon.</p>
                </div>
              </div>
              <div class="group">
                <img
                  src="~/assets/img/man.png"
                  width="300"
                  height="300"
                  style=""
                  alt="Attraction"
                  class="mx-auto aspect-square overflow-hidden rounded-xl object-cover object-center transition-all group-hover:scale-105"
                />
                <div class="mt-4 space-y-1">
                  <h3 class="text-lg font-bold">Eiffel Tower</h3>
                  <p class="text-muted-foreground">Marvel at the iconic Eiffel Tower in Paris.</p>
                </div>
              </div>
              <div class="group">
                <img
                  src="~/assets/img/man.png"
                  width="300"
                  height="300"
                  alt="Attraction"
                  style=""
                  class="mx-auto aspect-square overflow-hidden rounded-xl object-cover object-center transition-all group-hover:scale-105"
                />
                <div class="mt-4 space-y-1">
                  <h3 class="text-lg font-bold">Machu Picchu</h3>
                  <p class="text-muted-foreground">Discover the ancient Inca citadel of Machu Picchu.</p>
                </div>
              </div>
              <div class="group">
                <img
                  src="~/assets/img/man.png"
                  width="300"
                  height="300"
                  style=""
                  alt="Attraction"
                  class="mx-auto aspect-square overflow-hidden rounded-xl object-cover object-center transition-all group-hover:scale-105"
                />
                <div class="mt-4 space-y-1">
                  <h3 class="text-lg font-bold">Taj Mahal</h3>
                  <p class="text-muted-foreground">Experience the timeless beauty of the Taj Mahal.</p>
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
  
  <script setup lang="ts">
  definePageMeta({
      middleware: "already-logged-in",
  });
  
  useHead({ title: "Welcome" });
  </script>
  
  <style></style>
  