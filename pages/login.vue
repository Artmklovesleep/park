<template>
    <UContainer class="flex items-center justify-center h-screen bg-background">
        <div class="w-full max-w-md p-6 space-y-6 bg-card rounded-lg shadow-lg">
            <NuxtLink to="/">
                <img src="~/assets/img/kachel.png"
                    class="sm:w-64 mx-auto w-32 backdrop-blur-sm animate__animated animate__swing" alt="" />
            </NuxtLink>
            <div class="space-y-2 text-center">
                <h1 class="text-3xl font-bold tracking-tight text-black">
                    Войдите в свой аккаунт
                </h1>
                <p class="text-muted-foreground text-gray-600">
                    Войдите в свой аккаунт, чтобы продолжить.
                </p>
            </div>
            <UForm :schema="schema" :state="state" class="space-y-4" @submit="handleSubmit($event, state)">
                <UFormGroup label="Электронная почта" name="email">
                    <UInput id="email" v-model="state.email" placeholder="primer@mail.ru" class="font-bold text-black"
                        :ui="{ placeholder: 'placeholder-gray-400' }" />
                </UFormGroup>

                <UFormGroup label="Пароль" name="password">
                    <UInput id="password" v-model="state.password" type="password" placeholder=""
                        class="font-semibold text-black" />
                </UFormGroup>

                <button type="submit"
                    class="w-full text-white bg-black hover:bg-gray-800 focus:outline-none focus:ring-gray-800 shadow-lg shadow-gray-500/50 dark:shadow-lg dark:shadow-gray-700/80 font-medium rounded-lg text-sm px-5 py-2.5 mb-2 animate__animated transition ease-in-out duration-300">
                    Войти
                </button>
            </UForm>
            <div class="mt-4 flex flex-row">
                <div class="font-semibold my-auto leading-4 text-black">
                    <NuxtLink to="register" class="text-black">Нет аккаунта?</NuxtLink>
                </div>
                <NuxtLink to="register"
                    class="text-center bg-transparent hover:bg-gray-200 my-auto shadow-lg dark:shadow-neutral-700/50 grow text-black font-semibold p-1 border-2 border-black dark:border-neutral-400 hover:dark:bg-neutral-800 rounded-lg animate__animated hover:animate__swing ml-3">
                    Зарегистрироваться</NuxtLink>
            </div>
        </div>
    </UContainer>
</template>

<script setup lang="ts">
import type { FormError, FormSubmitEvent } from "#ui/types";
import { z } from "zod";

definePageMeta({
    middleware: "already-logged-in",
})

useHead({ title: "Login" });

const schema = z.object({
    email: z.string().email("Invalid email"),
    password: z.string().min(6, "Must be at least 6 characters"),
});

const state = reactive({
    email: undefined,
    password: undefined,
});

const { login } = actions();

const handleSubmit = async (event: FormSubmitEvent<any>, state: any) => {
    try {
        await login(state.email, state.password);
    } catch (error) {
        console.log(error);
    }
};
</script>
