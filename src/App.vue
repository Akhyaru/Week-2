<script setup lang="ts">
import { useRouter } from "vue-router";
import { useAuthStore } from "@/stores/auth";

const auth = useAuthStore();
const router = useRouter();

const onLogout = () => {
  auth.logout();
  router.push("/login");
};

const showAlert = () => {
  alert("Anda harus login untuk mengakses halaman ini!");
};
</script>

<template>
  <div class="bg-blue-500">
    <div class="container mx-auto p-4">
      <div class="flex justify-between items-center">
        <!-- Logo and Title -->
        <div class="text-2xl font-bold text-white">Week 2</div>

        <!-- Navigation Menu -->
        <div class="flex gap-4">
          <router-link to="/" class="text-white hover:underline">Home</router-link>
          <router-link to="/about" class="text-white hover:underline">About</router-link>

          <template v-if="auth.username">
            <router-link to="/restricted" class="text-white hover:underline">Restricted Page</router-link>
          </template>
          
          <template v-else>
            <p class="text-white cursor-pointer" @click="showAlert">Restricted Page</p>
          </template>
        </div>

        <!-- Authenticated User -->
        <div class="flex items-center gap-2">
          <template v-if="auth.username">
            <p class="text-white">{{ auth.username }}</p>
            <button @click="onLogout" class="bg-red-500 text-white py-1 px-3 rounded-md hover:bg-red-600">
              Logout
            </button>
          </template>

          <template v-else>
            <router-link to="/login" class="bg-green-500 text-white py-1 px-3 rounded-md hover:bg-green-600">
              Login
            </router-link>
          </template>
        </div>
      </div>
    </div>
  </div>

  <!-- Body -->
  <div class="container mx-auto p-4">
    <router-view></router-view>
  </div>
</template>