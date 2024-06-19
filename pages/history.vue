<template>
    <div v-if="tickets.length" class="mt-6">
            <h2 class="text-2xl font-bold mb-4">Orders</h2>
            <div v-for="ticket in tickets" :key="ticket.ticketId" class="mb-6 p-4 border border-gray-300 rounded-md">
                <h3 class="text-xl font-semibold">Order ID: {{ ticket.ticketId }}</h3>
                <p class="text-gray-700">Status: {{ ticket.status }}</p>
                <p class="text-gray-700">Payment Date: {{ new Date(ticket.datePayment).toLocaleDateString() }}</p>
                <h4 class="text-lg font-medium mt-4">Items:</h4>
                <ul class="list-disc list-inside">
                    <li v-for="item in ticket.ticketItems" :key="item.ticketItemId" class="mt-2">
                        <p class="text-gray-800">Attraction: {{ item.attractionName }}</p>
                        <p class="text-gray-800">Quantity: {{ item.quantity }}</p>
                        <p class="text-gray-800">Price: {{ item.price }} руб.</p>
                    </li>
                </ul>
            </div>
        </div>
</template>

<script setup>
import { ref } from 'vue';

import { API } from '~/plugins/axios.js'; 

const user = useCurrentUser();
const userdb = ref({});
const tickets = ref([]);
console.log(user);
get_user_data();

function get_user_data() {
    if (user.value?.email) {
        API.get(`Clients/by-email/${user.value.email}`)
            .then(response => {
                userdb.value = response.data;
                console.log('User Data:', userdb.value);
                
                API.get(`Tickets/client/${userdb.value.clientId}`)
                    .then(response => {
                        tickets.value = response.data;
                        console.log('Tickets Data:', tickets.value);
                    })
                    .catch(error => {
                        console.error('Ошибка при выполнении запроса Tickets:', error);
                    });
            })
            .catch(error => {
                console.error('Ошибка при выполнении запроса Clients:', error);
            });
    }
}

definePageMeta({
    layout: "admin",
    middleware: "auth",
});

useHead({ title: "Settings" });



const { logout } = actions();
</script>
