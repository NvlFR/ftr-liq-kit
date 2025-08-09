<script setup>
import { Head, useForm } from '@inertiajs/vue3';
import GuestLayout from '@/Layouts/GuestLayout.vue';
import { QCard, QCardSection, QForm, QInput, QBtn, QBanner } from 'quasar';

const form = useForm({
    name: '',
    email: '',
    password: '',
    password_confirmation: '',
});

const submit = () => {
    form.post(route('register'), {
        onFinish: () => form.reset('password', 'password_confirmation'),
    });
};
</script>

<template>
    <GuestLayout>
        <Head title="Register" />

        <q-banner v-if="form.hasErrors" inline-actions class="text-white bg-red q-mb-md">
            Oops! Ada yang salah. Silakan periksa kembali isian Anda.
        </q-banner>

        <q-card class="my-card">
            <q-card-section>
                <div class="text-h6 text-center">Buat Akun Baru</div>
                <div class="text-subtitle2 text-center">Isi data di bawah untuk mendaftar</div>
            </q-card-section>

            <q-card-section>
                <q-form @submit.prevent="submit" class="q-gutter-md">
                    <q-input
                        filled
                        v-model="form.name"
                        label="Nama Lengkap"
                        lazy-rules
                        :error="form.errors.name ? true : false"
                        :error-message="form.errors.name"
                        autocomplete="name"
                    />

                    <q-input
                        filled
                        v-model="form.email"
                        label="Alamat Email"
                        lazy-rules
                        :error="form.errors.email ? true : false"
                        :error-message="form.errors.email"
                        type="email"
                        autocomplete="username"
                    />

                    <q-input
                        filled
                        v-model="form.password"
                        label="Password"
                        lazy-rules
                        :error="form.errors.password ? true : false"
                        :error-message="form.errors.password"
                        type="password"
                        autocomplete="new-password"
                    />

                    <q-input
                        filled
                        v-model="form.password_confirmation"
                        label="Konfirmasi Password"
                        lazy-rules
                        type="password"
                        autocomplete="new-password"
                    />

                    <div class="flex items-center justify-between q-mt-lg">
                        <a :href="route('login')" class="text-grey-8">
                            Sudah punya akun?
                        </a>

                        <q-btn
                            label="Register"
                            type="submit"
                            color="primary"
                            :loading="form.processing"
                        />
                    </div>
                </q-form>
            </q-card-section>
        </q-card>
    </GuestLayout>
</template>