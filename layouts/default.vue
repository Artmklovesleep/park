<template>
	<ClientOnly
		></ClientOnly>

	<slot />
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
</script>

<style></style>
