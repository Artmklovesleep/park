<template>
    <UContainer class="grid place-content-center h-screen bg-white">
        <div class="w-full max-w-md p-6 space-y-6 bg-card rounded-lg shadow-lg">
        <div class="flex-col px-6">
            <div class="sm:mx-auto sm:w-full sm:max-w-sm">
                <h2 class="my-3 text-center text-3xl font-bold leading-9 tracking-tight text-black">
                    Зарегистрируйте свой личный аккаунт
                </h2>
            </div>
            <div class="sm:mx-auto sm:w-full sm:max-w-sm mb-10">
                <UForm :schema="schema" :state="state" class="space-y-4" @submit="handleSubmit($event, state)">
                    <UFormGroup label="Nickname" name="nickname">
                        <UInput 
                            v-model="state.nickname" 
                            placeholder="" 
                            class="font-bold text-black" 
                            :ui="{
                                placeholder: 'placeholder-gray-400',
                            }"
                        />
                    </UFormGroup>

                    <UFormGroup label="Электронная почта" name="email">
                        <UInput 
                            v-model="state.email" 
                            placeholder="primer@mail.ru" 
                            class="font-bold text-black" 
                            :ui="{
                                placeholder: 'placeholder-gray-400',
                            }"
                        />
                    </UFormGroup>

                    <UFormGroup label="Пароль" name="password">
                        <UInput 
                            v-model="state.password" 
                            type="password" 
                            placeholder="" 
                            class="font-semibold text-black" 
                        />
                    </UFormGroup>

                    <div class="flex flex-row">
                        <button
                            class="grow text-white bg-black hover:bg-gray-800 focus:outline-none focus:ring-gray-800 shadow-lg shadow-gray-500/50 dark:shadow-lg dark:shadow-gray-700/80 font-medium rounded-lg text-sm px-5 py-2.5 mb-2 animate__animated transition ease-in-out duration-300"
                        >
                            Зарегистрироваться
                        </button>
                    </div>
                </UForm>
                <div class="mt-4 flex flex-row">
                    <div class="font-semibold my-auto leading-4 text-black">
                        <NuxtLink href="login" class="text-black">Уже есть аккаунт?</NuxtLink>
                    </div>
                    <NuxtLink
                        to="login"
                        class="text-center bg-transparent hover:bg-gray-200 my-auto shadow-lg dark:shadow-neutral-700/50 grow text-black font-semibold p-1 border-2 border-black dark:border-neutral-400 hover:dark:bg-neutral-800 rounded-lg animate__animated hover:animate__swing ml-3"
                    >
                        Войти
                    </NuxtLink>
                </div>
            </div>
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

useHead({ title: "Registration" });

type Schema = z.output<typeof schema>;

const schema = z.object({
    nickname: z.string().min(6, "Must be at least 6 characters").max(25),
    email: z.string().email("Invalid email"),
    password: z.string().min(6, "Must be at least 6 characters"),
});

const state = reactive({
    nickname: undefined,
    email: undefined,
    password: undefined,
});

const { register } = actions();

const handleSubmit = async (event: FormSubmitEvent<any>, state: any) => {

    try {
        await register(state.email, state.password, state.nickname);
    } catch (error) {
        console.log(error);
    }
};
</script>
