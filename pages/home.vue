<template>
    <section id="attractions" class="w-full bg-muted flex flex-col">
        <div class="w-full mx-auto px-4 sm:px-6 lg:px-8">
            <div class="flex flex-col items-center justify-center space-y-4 text-center">
                <div class="space-y-2">
                    <h2 class="text-3xl font-bold tracking-tighter sm:text-5xl">Наши аттракционы</h2>
                    <p
                        class="max-w-[900px] text-muted-foreground md:text-xl/relaxed lg:text-base/relaxed xl:text-xl/relaxed">
                        От захватывающих природных чудес до захватывающих приключений, наша подобранная коллекция лучших
                        достопримечательностей предлагает что-то для каждого.
                    </p>
                </div>
            </div>
            <div class="mx-auto grid grid-cols-1 gap-6 py-12 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4">
                <div v-for="attraction in Attractions.results" :key="attraction.attractionId" class="group">
                    <img :src="`${attraction.nameAttraction}.jpg`" width="300" height="300" :alt="attraction.nameAttraction"
                        class="mx-auto aspect-square overflow-hidden rounded-xl object-cover object-center transition-all" />
                    <div class="mt-4 space-y-1">
                        <h3 class="text-lg font-bold">{{ attraction.nameAttraction }}</h3>
                        <p class="text-muted-foreground">{{ attraction.description }}</p>
                    </div>
                    <div class="flex flex-row w-full">
                        <button v-if="attraction.quantity == None"
                            class="btn__green w-full animate__animated animate__fadeIn" @click="addToCart(attraction)">В
                            корзину</button>
                        <button v-if="attraction.quantity > 0" @click="navigateTo('/orders')"
                            class="btn__green-disabled w-full animate__animated animate__fadeIn">В
                            корзинe</button>
                    </div>

                </div>
            </div>
        </div>
        <button v-if="totalItems > 0" @click="navigateTo('/orders')"
            class="btn__green animate__animated animate__pulse pulse w-64 self-center">Перейти в
            корзину</button>
    </section>
</template>

<script setup>
definePageMeta({
    layout: "admin",
    middleware: "auth",
});

const cartStore = useCartStore();
const { items: cartItems, totalItems, totalPrice } = storeToRefs(cartStore);
import { ref } from 'vue';
import { API } from '~/plugins/axios.js';
import { useCartStore } from '~/stores/cart';
import { storeToRefs } from 'pinia';

const Attractions = ref({ results: [] });

Attractions.value.results = [
    {
        "attractionId": 1,
        "nameAttraction": "Емеля",
        "capacity": 30,
        "price": 500,
        "description": "Заватывающий аттракцион Емеля",
    },
    {
        "attractionId": 2,
        "nameAttraction": "Карусель",
        "capacity": 20,
        "price": 300,
        "description": "Захватывающий аттракцион Карусель",
    },
    {
        "attractionId": 3,
        "nameAttraction": "Колесо обозрения",
        "capacity": 35,
        "price": 1000,
        "description": "Захватывающий аттракцион Колесо обозрения",
    },
    {
        "attractionId": 4,
        "nameAttraction": "Американские горки",
        "capacity": 15,
        "price": 560,
        "description": "Захватывающий аттракцион Американские горки",
    }
]
function update_attraction() {
    for (let i = 0; i < cartItems.value.length; i++) {
        for (let j = 0; j < Attractions.value.results.length; j++) {
            if (cartItems.value[i].id == Attractions.value.results[j].attractionId) {
                Attractions.value.results[j].quantity = cartItems.value[i].quantity;
            }
        }
    }
}

update_attraction();
// get_Attractions_data();

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

function addToCart(attraction) {
    cartStore.addItem({
        id: attraction.attractionId,
        title: attraction.nameAttraction,
        price: attraction.price,
        quantity: 1,
    });
    update_attraction();
    // console.log(cartItems.value);
}

const { logout } = actions();
</script>
