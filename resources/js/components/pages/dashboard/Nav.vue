<template>
    <nav
        class="nav w-80 p-4 flex flex-col justify-between border-2 border-dashed border-red-500 mr-4 rounded-xl overflow-auto">
        <div>
            <img src="@/assets/medal.svg" alt="" class="block w-14 mx-auto pb-4 cursor-pointer"
                 @click="router.push({name: 'user_main'})">

            <div class="text-white">
                <div class="user-links mb-4">
                    <a @click="router.push({name: 'user_main'})"
                       class="block font-bold bg-green-600 mb-2 px-4 py-2 rounded-xl hover:bg-green-500 transition duration-300 ease-in-out hover:shadow-md cursor-pointer">Главная</a>
                    <a @click="router.push({name: 'user_events'})"
                       class="block font-bold bg-green-600 px-4 py-2 rounded-xl hover:bg-green-500 transition duration-300 ease-in-out hover:shadow-md cursor-pointer">Новости</a>
                </div>

                <div class="admin-menu bg-zinc-800 p-2 rounded-xl" v-show="userStore.user[0].role === 'admin'">
                    <span class="block font-bold mb-2 text-center">Админка</span>
                    <div class="admin-links">
                        <a @click="router.push({name: 'admin_main'})"
                           class="block font-bold bg-blue-600 mb-2 px-4 py-2 rounded-xl hover:bg-blue-400 transition duration-300 ease-in-out hover:shadow-md cursor-pointer">Главная</a>
                        <a @click="router.push({name: 'admin_users'})"
                           class="block font-bold bg-blue-600 mb-2 px-4 py-2 rounded-xl hover:bg-blue-400 transition duration-300 ease-in-out hover:shadow-md cursor-pointer">Пользователи</a>
                        <a @click="router.push({name: 'admin_trophies'})"
                           class="block font-bold bg-blue-600 mb-2 px-4 py-2 rounded-xl hover:bg-blue-400 transition duration-300 ease-in-out hover:shadow-md cursor-pointer">Трофеи</a>
                        <a @click="router.push({name: 'admin_events'})"
                           class="block font-bold bg-blue-600 px-4 py-2 rounded-xl hover:bg-blue-400 transition duration-300 ease-in-out hover:shadow-md cursor-pointer">Новости</a>
                    </div>
                </div>
            </div>
        </div>

        <div class="user bg-red-600 p-2 mt-4 rounded-xl shadow-md">
            <div class="flex items-center justify-between mb-2">
                <img src="@/assets/medal.svg" alt="" class="inline-block w-8 bg-white rounded-3xl">
                <span
                    class="block text-white font-bold italic">{{
                        `${userStore.user[0].first_name} ${userStore.user[0].last_name[0]}.`
                    }}
                </span>
            </div>
            <a href="#"
               class="block bg-green-600 text-white text-center font-bold px-4 py-1 rounded-xl hover:bg-green-500 transition duration-300 ease-in-out hover:shadow-md"
               @click.prevent="logout"
            >
                Выйти
            </a>
        </div>
    </nav>
</template>

<script setup>
import {useRouter} from 'vue-router';
import {useUserStore} from '@/stores/user.js';

const router = useRouter();
const userStore = useUserStore();

function logout() {
    axios.post('/logout').then(response => {
        localStorage.removeItem('isAuthenticated');
        localStorage.removeItem('userEmail')
        router.push({name: 'login'});
    })
}
</script>

<style lang="scss" scoped>

</style>
