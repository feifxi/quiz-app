<script setup>
import { RouterLink } from 'vue-router';
import { useAuthStore } from '@/stores/user';

const authStore = useAuthStore()

const logout = () => {
    authStore.setAuthUser(null)
    localStorage.removeItem('userId')
    location.replace(import.meta.env.BASE_URL);
}
</script>

<template>
    <header
        class="font-extrabold flex justify-between items-center text-white px-10 py-3 bg-green-500 border-b-3 border-green-600">
        <RouterLink to="/">
            <h2 class="text-3xl font-bold cursor-pointer hover:scale-110">QUIZZA</h2>
        </RouterLink>
        <nav v-if="authStore.isAuthenticated" class="flex items-center gap-5">
            <RouterLink to="/workspace" class="hover:underline cursor-pointer">Workspace</RouterLink>
            <RouterLink to="/leaderboard" class="hover:underline cursor-pointer">Leaderboard</RouterLink>
            <RouterLink to="/profile">
                <div class="flex items-center  ">
                    <div class="border-1 rounded-full w-12.5 h-12.5 mx-auto flex items-center justify-center relative border-black"
                        :style="{
                            backgroundImage: 'linear-gradient(to ' + (authStore.authUser.profileFrame?.selectedMode || 'top') + ','
                                + (authStore.authUser.profileFrame?.color1 || 'lime') + ',' + (authStore.authUser.profileFrame?.color2 || 'lime')
                                + ',' + (authStore.authUser.profileFrame?.color3 || 'lime') + ',' + (authStore.authUser.profileFrame?.color4 || 'lime')
                                + ',' + (authStore.authUser.profileFrame?.color5 || 'lime') + ')'
                        }">
                        >
                        <img :src="authStore.authUser.profilePic || 'https://img.myloview.com/posters/default-avatar-profile-icon-vector-social-media-user-photo-700-205577532.jpg'"
                            alt="profilepic"
                            class=" w-10 h-10 rounded-full object-cover absolute border-1 border-black">
                    </div>

                </div>
            </RouterLink>
            <button @click="logout" class="hover:underline cursor-pointer">Logout</button>
        </nav>
        <nav v-else class="flex gap-5">
            <RouterLink to="/signin" class="hover:underline cursor-pointer">Sign In</RouterLink>
            <RouterLink to="/signup" class="hover:underline cursor-pointer">Sign Up</RouterLink>
        </nav>
    </header>
</template>

<style scoped></style>