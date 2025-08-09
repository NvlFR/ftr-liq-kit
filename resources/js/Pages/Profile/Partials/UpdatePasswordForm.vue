<script setup>
import { useForm } from '@inertiajs/vue3';
import { ref } from 'vue';
import { QCard, QCardSection, QForm, QInput, QBtn } from 'quasar';

const passwordInput = ref(null);
const currentPasswordInput = ref(null);

const form = useForm({
    current_password: '',
    password: '',
    password_confirmation: '',
});

const updatePassword = () => {
    form.put(route('password.update'), {
        preserveScroll: true,
        onSuccess: () => form.reset(),
        onError: () => {
            if (form.errors.password) {
                form.reset('password', 'password_confirmation');
                passwordInput.value.focus();
            }
            if (form.errors.current_password) {
                form.reset('current_password');
                currentPasswordInput.value.focus();
            }
        },
    });
};
</script>

<template>
     <q-card>
        <q-card-section>
            <div class="text-h6">Ubah Kata Sandi</div>
            <div class="text-subtitle2">Pastikan akun Anda menggunakan kata sandi yang panjang dan acak agar tetap aman.</div>
        </q-card-section>

        <q-card-section>
            <q-form @submit.prevent="updatePassword" class="q-gutter-md">
                <q-input
                    ref="currentPasswordInput"
                    filled
                    v-model="form.current_password"
                    label="Kata Sandi Saat Ini"
                    type="password"
                    :error="form.errors.current_password ? true : false"
                    :error-message="form.errors.current_password"
                />

                <q-input
                    ref="passwordInput"
                    filled
                    v-model="form.password"
                    label="Kata Sandi Baru"
                    type="password"
                    :error="form.errors.password ? true : false"
                    :error-message="form.errors.password"
                />

                <q-input
                    filled
                    v-model="form.password_confirmation"
                    label="Konfirmasi Kata Sandi Baru"
                    type="password"
                    :error="form.errors.password_confirmation ? true : false"
                    :error-message="form.errors.password_confirmation"
                />

                <div class="flex items-center q-gutter-x-sm">
                    <q-btn label="Simpan" type="submit" color="primary" :loading="form.processing" />
                    <transition
                        enter-active-class="animated fadeIn"
                        leave-active-class="animated fadeOut"
                    >
                        <div v-if="form.recentlySuccessful" class="text-grey-8">Tersimpan.</div>
                    </transition>
                </div>
            </q-form>
        </q-card-section>
    </q-card>
</template>