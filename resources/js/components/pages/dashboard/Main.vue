<template>
    <div>
        <div>
            {{ userStore.user }}
        </div>
        <router-view></router-view>
    </div>
</template>

<script setup>
import {onMounted} from "vue";
import {useUserStore} from '@/stores/user.js';

const userStore = useUserStore();

onMounted(() => {
    userStore.getInfoUser(localStorage.getItem('userEmail'));
})
</script>

<style lang="scss" scoped>

</style>
