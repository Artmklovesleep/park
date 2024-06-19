<template>
    <div class="flex flex-col h-screen">
        <sidebar></sidebar>
        <slot />
    </div>

    <ClientOnly>
        
    </ClientOnly>
    <UNotifications />
</template>

<script setup lang="ts">
const colorMode = useColorMode();
const isDark = computed({
    get() {
        return colorMode.value === "dark";
    },
    set() {
        colorMode.preference = colorMode.value === "dark" ? "light" : "dark";
    },
});

let open = false;
const toggle = () => {
    open = !open;
    console.log(open);
};


const links = [
    {
        label: "Profile",
        avatar: {
            src: "https://avatars.githubusercontent.com/u/739984?v=4",
        },
        badge: 100,
    },
    {
        label: "Installation",
        icon: "i-heroicons-home",
        to: "/home",
    },
    {
        label: "Vertical Navigation",
        icon: "i-heroicons-chart-bar",
        to: `/home`,
    },
    {
        label: "Command Palette",
        icon: "i-heroicons-command-line",
        to: "/home",
    },
];
</script>
