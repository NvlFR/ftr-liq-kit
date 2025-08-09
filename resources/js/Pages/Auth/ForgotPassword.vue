<script setup>
import { Head, useForm } from '@inertiajs/vue3';
import GuestLayout from '@/Layouts/GuestLayout.vue';
import { QCard, QCardSection, QForm, QInput, QBtn, QBanner } from 'quasar';

// 'status' adalah prop yang dikirim oleh Laravel setelah email berhasil dikirim
defineProps({
    status: String,
});

const form = useForm({
    email: '',
});

const submit = () => {
    form.post(route('password.email'));
};
</script>

<template>
    <GuestLayout>
        <Head title="Forgot Password" />

        <q-card class="my-card">
            <q-card-section>
                <div class="text-subtitle2">
                    Lupa password Anda? Tidak masalah. Beri tahu kami alamat email Anda dan kami akan mengirimkan link untuk mengatur ulang password Anda.
                </div>
            </q-card-section>

            <q-card-section>
                <q-banner v-if="status" inline-actions class="text-white bg-green q-mb-md">
                    {{ status }}
                </q-banner>

                <q-form @submit.prevent="submit" class="q-gutter-md">
                    <q-input
                        filled
                        v-model="form.email"
                        label="Alamat Email"
                        lazy-rules
                        :error="form.errors.email ? true : false"
                        :error-message="form.errors.email"
                        type="email"
                    />

                    <div class="flex justify-end q-mt-lg">
                         <q-btn
                            label="Kirim Link Reset Password"
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