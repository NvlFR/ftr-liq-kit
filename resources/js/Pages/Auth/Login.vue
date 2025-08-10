<script setup>
import { handleSubmit } from "@/helpers/client-req-handler";
import { useForm } from "@inertiajs/vue3";
import { ref } from "vue";

let form = useForm({
  username: window.CONFIG.APP_DEMO ? "admin" : "",
  password: window.CONFIG.APP_DEMO ? "12345" : "",
  remember: true,
});

const submit = () => handleSubmit({ form, url: route("admin.auth.login") });
const showPassword = ref(false);
</script>

<template>
  <i-head title="Login" />
  <guest-layout>
    <q-page class="row justify-center items-center bg-gradient">
      <q-form class="q-gutter-md" @submit.prevent="submit">
        <q-card flat bordered class="q-pa-lg shadow-card">
          <q-card-section class="text-center">
            <q-avatar size="90px" >
              <img src="/assets/img/app-logo.png" />
            </q-avatar>
            <h5 class="q-my-sm text-primary">Selamat Datang</h5>
            <p class="text-subtitle2 text-grey-7">Masuk ke akun Anda</p>
          </q-card-section>

          <q-card-section>
            <q-input
              v-model.trim="form.username"
              label="Username"
              lazy-rules
              :error="!!form.errors.username"
              autocomplete="username"
              :error-message="form.errors.username"
              :disable="form.processing"
              :rules="[
                val => (val && val.length > 0) || 'Masukkan Username',
              ]"
            >
              <template #append>
                <q-icon name="person" />
              </template>
            </q-input>

            <q-input
              v-model="form.password"
              :type="showPassword ? 'text' : 'password'"
              label="Kata Sandi"
              :error="!!form.errors.password"
              autocomplete="current-password"
              :error-message="form.errors.password"
              lazy-rules
              :disable="form.processing"
              :rules="[
                val => (val && val.length > 0) || 'Masukkan kata sandi',
              ]"
              class="q-mt-md"
            >
              <template #append>
                <q-btn
                  dense
                  flat
                  round
                  @click="showPassword = !showPassword"
                >
                  <q-icon :name="showPassword ? 'visibility_off' : 'visibility'" />
                </q-btn>
              </template>
            </q-input>

            <q-checkbox
              v-model="form.remember"
              :disable="form.processing"
              label="Ingat saya di perangkat ini"
              class="q-mt-sm"
            />
          </q-card-section>

          <q-card-actions>
            <q-btn
              icon="login"
              type="submit"
              color="primary"
              class="full-width q-py-sm btn-hover"
              label="Login"
              :disable="form.processing"
            />
          </q-card-actions>
        </q-card>
      </q-form>
    </q-page>
  </guest-layout>
</template>

<style scoped>


.shadow-card {
  border-radius: 16px;
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.12);
  width: 360px;
  background-color: white;
}

.bg-avatar {
  background-color: rgba(2, 209, 208, 0.1);
}

.btn-hover:hover {
  transform: translateY(-2px);
  box-shadow: 0 4px 12px rgba(2, 209, 208, 0.4);
  transition: all 0.2s ease;
}
</style>
