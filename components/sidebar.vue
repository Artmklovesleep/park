<template>
    <div class="flex flex-col min-h-screen top-0 w-full">
        <!-- Navigation Bar -->
        <nav class="bg-white dark:bg-pale-sky-900 px-5 py-3 shadow-md">
            <div class="flex justify-between items-center">
                <div class="flex space-x-4">
                    <div v-for="link in links" :key="link.label"
                        class="cursor-pointer px-3 py-2 rounded-md text-sm font-medium" :class="{
                            'bg-pale-sky-900 text-white': isActive(link.to),
                            'text-pale-sky-500 hover:text-pale-sky-900 dark:text-pale-sky-400 hover:dark:text-white':
                                !isActive(link.to)
                        }" @click="navigate(link.to)">
                        <span v-if="link.icon" :class="link.icon"></span>
                        {{ link.label }}
                    </div>
                </div>
                <button type="submit" @click="logout"
                    class="h-9 px-3 text-white active:bg-pale-sky-900 hover:bg-pale-sky-800 bg-pale-sky-900 shadow-lg dark:shadow-neutral-700/50 text-black-700 font-semibold border-2 border-pale-sky-900 dark:border-neutral-100 hover:dark:bg-neutral-200 dark:bg-neutral-50 dark:text-black active:dark:bg-neutral-50 rounded-lg">
                    Выйти
                </button>
            </div>
        </nav>
        <!-- Page Content -->
        <main class="flex-1 p-5">
            <router-view></router-view>
        </main>
    </div>
</template>
  

<script setup lang="ts">
import { ref } from 'vue';
import { useRouter, useRoute } from 'vue-router';


const user = useCurrentUser();
const router = useRouter();
const route = useRoute();

const links = [
    {
        label: user.value?.displayName,
        avatar: {
            // src: "https://avatars.githubusercontent.com/u/739984?v=4",
        },
        to: "/profile",
        badge: 100,
    },
    {
        label: "Главная",
        icon: "i-heroicons-home",
        to: "/home",
    },
    {
        label: "Настройки",
        icon: "i-heroicons-chart-bar",
        to: `/settings`,
    },
    {
        label: "Заказы",
        icon: "i-heroicons-shopping-bag-solid",
        to: "/orders",
    },

];

const { logout } = actions();

function navigate(to: string) {
    router.push(to);
}

function isActive(to: string) {
    return route.path === to;
}
</script>
  