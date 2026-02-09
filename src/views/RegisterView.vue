<template>
  <div class="min-h-screen flex items-center justify-center bg-gray-100">
    <div class="p-6 bg-white rounded-lg shadow-lg w-full max-w-sm">
      <h2 class="text-2xl font-semibold mb-4 text-center">Kayıt Ol</h2>

      <form @submit.prevent="handleRegister" class="space-y-3">
        <input
          v-model="username"
          placeholder="Kullanıcı adı"
          class="w-full p-2 border rounded focus:outline-none focus:ring-2 focus:ring-green-500"
        />
        <input
          v-model="password"
          type="password"
          placeholder="Şifre"
          class="w-full p-2 border rounded focus:outline-none focus:ring-2 focus:ring-green-500"
        />
        <button
          type="submit"
          class="w-full bg-green-500 text-white p-2 rounded hover:bg-green-600"
        >
          Kayıt Ol
        </button>
      </form>

      <p class="mt-4 text-center text-gray-600">
        Zaten hesabın var mı?
        <span
          @click="goToLogin"
          class="text-blue-500 hover:underline cursor-pointer"
        >
          Giriş Yap
        </span>
      </p>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";
import { useAuthStore } from "../stores/authStore";
import { useRouter } from "vue-router";

const username = ref("");
const password = ref("");
const authStore = useAuthStore();
const router = useRouter();

async function handleRegister() {
  const success = await authStore.register(username.value, password.value);
  if (success) {
    alert("Kayıt başarılı! Giriş sayfasına yönlendiriliyorsunuz.");
    router.push("/welcome"); // login sayfasına yönlendir
  } else {
    alert("Bu kullanıcı adı zaten mevcut!");
  }
}

function goToLogin() {
  router.push("/welcome"); // login sayfasına geri dön
}
</script>
