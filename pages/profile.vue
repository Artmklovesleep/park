<template>
    <div class="grow grid place-content-center">
        <div class="flex flex-col items-center">
            <div class="text-3xl">Ваши личные данные</div>
            <form class="flex flex-col items-center space-y-4 mt-4" @submit.prevent="putUserData">
                <input type="text" v-model="firstName" placeholder="Имя" class="border rounded p-2">
                <input type="text" v-model="lastName" placeholder="Фамилия" class="border rounded p-2">
                <input type="text" v-model="middleName" placeholder="Отчество" class="border rounded p-2">
                <input type="tel" v-model="phoneNumber" placeholder="Номер телефона" class="border rounded p-2">
                <button type="submit" class="bg-black text-white rounded p-2 mt-4">Submit</button>
            </form>
        </div>
    </div>
</template>

<script setup lang="ts">

import { ref } from 'vue';

import { API } from '~/plugins/axios.js'; 

const user = useCurrentUser();
const userdb = ref({
    surname: "",
    name: "",
    lastname: "",
    phone: "",
});

const firstName = ref("");
const lastName = ref("");
const middleName = ref("");
const phoneNumber = ref("");

console.log(user);
get_user_data();

function get_user_data() {
    if (user.value?.email) {
        API.get(`Clients/by-email/${user.value.email}`)
            .then(response => {
                userdb.value = response.data;
                console.log(userdb.value);

                // Populate the input fields
                firstName.value = userdb.value.name || "";
                lastName.value = userdb.value.surname || "";
                middleName.value = userdb.value.lastname || "";
                phoneNumber.value = userdb.value.phone || "";
            })
            .catch(error => {
                console.error('Ошибка при выполнении запроса:', error);
            });
    }
}


function putUserData() {
    if (user.value?.email) {
        const updatedData = {
            clientId: userdb.value.clientId,
            surname: lastName.value,
            name: firstName.value,
            lastname: middleName.value,
            birthday: userdb.value.birthday,
            gender: userdb.value.gender,
            phone: phoneNumber.value,
            email: userdb.value.email,
        };

        API.put(`Clients/${userdb.value.clientId}`, updatedData)
            .then(response => {
                userdb.value = response.data;
                console.log('Updated user data:', userdb.value);
                get_user_data();
            })
            .catch(error => {
                console.error('Ошибка при выполнении запроса:', error);
            });
    }
}

definePageMeta({
    layout: "admin",
    middleware: "auth",
});

useHead({ title: "Profile" });

</script>
