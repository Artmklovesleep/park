<template>
    <div class="flex flex-row h-full justify-between p-52">
        <div v-if="cartItems.length > 0" class="flex flex-wrap gap-10 p-5 ">
            <div class="animate__animated animate__fadeIn flex flex-col gap-1 rounded-3xl bg-pale-sky-150 overflow-hidden w-56 h-[330px]"
                v-for="item in cartItems" :key="item" style="box-shadow: rgba(0, 0, 0, 0.1) 0px 10px 50px;">
                <img :src="`${item.title}.jpg`" width="w-full" height="150" :alt="item.title"
                    class="mx-auto aspect-square overflow-hidden object-cover object-center transition-all" />
                <div class="text-xl font-bold text-center">{{ item.title }} <div class="text-sm text-pale-sky-600 self-end">
                        {{
                            item.price }}руб./шт.</div>
                </div>
                <div class="flex flex-row w-full justify-center gap-4 text-2xl items-center">
                    <button
                        class="bg-black hover:bg-pale-sky-700 active:bg-black transition duration-150 text-white px-2.5 rounded-lg h-8"
                        @click="item.quantity--; cartStore.updateItemQuantity(item.id, item.quantity);">-</button>
                    <div class="text-xl">{{ item.quantity }}</div>
                    <button @click="item.quantity++"
                        class="bg-black hover:bg-pale-sky-700 active:bg-black transition duration-150 text-white px-2 rounded-lg h-8">+</button>
                </div>

                <!-- <div class="self-center">Всего: <span class="text-xl font-bold">{{ item.price * item.quantity }}руб</span></div> -->
            </div>
        </div>
        <div v-else class="self-center flex flex-col">
            <div class="text-4xl font-semibold mb-2">Корзина пуста</div>
            <button class="btn__black self-end" @click="navigateTo('/home')">К покупкам</button>
        </div>
        <div v-if="cartItems.length > 0" class="m-5 rounded-lg bg-pale-sky-800 self-center flex flex-col">

            <div class="flex flex-col border-b-2 border-pale-sky-700">
                <button class="btn__white m-5"
                    style="box-shadow: rgba(50, 50, 93, 0.25) 0px 30px 60px -12px inset, rgba(0, 0, 0, 0.3) 0px 18px 36px -18px inset;;">Купить
                    билеты</button>
            </div>
            <div class="text-pale-sky-200 m-5 flex flex-col gap-3">
                <div class="flex flex-row items-center justify-between gap-5">
                    <div class="text-xl font-bold">Ваша корзина</div>
                    <div>{{ totalItems }} билет(-ов)</div>
                </div>
                <div class="flex flex-row items-center justify-between gap-5">
                    <div>Товары ({{ totalItems }})</div>
                    <div class="text-xl font-bold">{{ totalPrice }}руб.</div>
                </div>
            </div>
        </div>
    </div>
</template>

<script setup>

const cartStore = useCartStore();
const { items: cartItems, totalItems, totalPrice } = storeToRefs(cartStore);
import { ref } from 'vue';
import { API } from '~/plugins/axios.js';
import { useCartStore } from '~/stores/cart';
import { storeToRefs } from 'pinia';

definePageMeta({
    layout: "admin",
    middleware: "auth",
});
useHead({ title: "Orders" });

function post_order() {



    cartStore.clearCart(); //конец функции
}

</script>
