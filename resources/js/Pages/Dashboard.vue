<script setup>
import AuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue';
import { Head } from '@inertiajs/vue3';
import { QCard, QCardSection } from 'quasar';
</script>

<template>
    <Head title="Dashboard" />

    <AuthenticatedLayout>
        <template #header>
            <h2 class="font-semibold text-xl text-gray-800 leading-tight">Dashboard</h2>
        </template>

        <q-card>
            <q-card-section>
                <div class="text-h6">Selamat Datang! 👋</div>
            </q-card-section>
            <q-card-section>
                Anda telah berhasil login. Ini adalah halaman utama Anda.
            </q-card-section>
        </q-card>
    </AuthenticatedLayout>
</template>