<script setup>
import { Link, useForm, usePage } from '@inertiajs/vue3';
import { QCard, QCardSection, QForm, QInput, QBtn, QBanner } from 'quasar';

defineProps({
    mustVerifyEmail: Boolean,
    status: String,
});

const user = usePage().props.auth.user;

const form = useForm({
    name: user.name,
    email: user.email,
});
</script>

<template>
    <q-card>
        <q-card-section>
            <div class="text-h6">Informasi Profil</div>
            <div class="text-subtitle2">Perbarui informasi profil dan alamat email akun Anda.</div>
        </q-card-section>

        <q-card-section>
            <q-form @submit.prevent="form.patch(route('profile.update'))" class="q-gutter-md">
                <q-input
                    filled
                    v-model="form.name"
                    label="Nama"
                    :error="form.errors.name ? true : false"
                    :error-message="form.errors.name"
                />

                <q-input
                    filled
                    v-model="form.email"
                    label="Email"
                    :error="form.errors.email ? true : false"
                    :error-message="form.errors.email"
                />

                <div v-if="mustVerifyEmail && user.email_verified_at === null">
                    <p class="text-sm q-mt-sm text-grey-8">
                        Alamat email Anda belum terverifikasi.
                        <Link
                            :href="route('verification.send')"
                            method="post"
                            as="button"
                            class="underline text-grey-6"
                        >
                            Klik di sini untuk mengirim ulang email verifikasi.
                        </Link>
                    </p>
                    <q-banner v-if="status === 'verification-link-sent'" inline-actions class="text-white bg-green q-mt-md">
                        Tautan verifikasi baru telah dikirim ke alamat email Anda.
                    </q-banner>
                </div>

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