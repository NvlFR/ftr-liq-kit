<script setup>
import { Head, useForm } from "@inertiajs/vue3";
import GuestLayout from "@/Layouts/GuestLayout.vue"; // Menggunakan layout khusus tamu
import {
    QCard,
    QCardSection,
    QForm,
    QInput,
    QCheckbox,
    QBtn,
    QBanner,
} from "quasar";

const form = useForm({
    email: "",
    password: "",
    remember: false,
});

const submit = () => {
    form.post(route("login"), {
        onFinish: () => form.reset("password"),
    });
};
</script>

<template>
    <GuestLayout>
        <Head title="Log in" />

        <q-banner
            v-if="form.hasErrors"
            inline-actions
            class="text-white bg-red q-mb-md"
        >
            Oops! Ada yang salah. Silakan periksa kembali isian Anda.
        </q-banner>

        <q-card class="my-card">
            <q-card-section>
                <div class="text-h6 text-center">Selamat Datang!</div>
                <div class="text-subtitle2 text-center">
                    Silakan masuk untuk melanjutkan
                </div>
            </q-card-section>

            <q-card-section>
                <q-form @submit.prevent="submit" class="q-gutter-md">
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
                        autocomplete="current-password"
                    />

                    <q-checkbox v-model="form.remember" label="Ingat saya" />

                    <div class="flex items-center justify-between q-mt-lg">
                        <a
                            :href="route('password.request')"
                            class="text-grey-8"
                        >
                            Lupa password?
                        </a>

                        <q-btn
                            label="Log In"
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
