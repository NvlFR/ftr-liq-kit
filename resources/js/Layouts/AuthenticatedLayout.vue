<script setup>
import { ref } from 'vue';
import { Head, Link } from '@inertiajs/vue3';
import {
    QLayout,
    QHeader,
    QToolbar,
    QToolbarTitle,
    QBtn,
    QDrawer,
    QList,
    QItem,
    QItemSection,
    QIcon,
    QPageContainer,
    QPage
} from 'quasar';

// State untuk mengontrol buka/tutup sidebar
const leftDrawerOpen = ref(true);

const toggleLeftDrawer = () => {
    leftDrawerOpen.value = !leftDrawerOpen.value;
};
</script>

<template>
    <Head title="Dashboard" />
    <q-layout view="hHh LpR fFf">

        <q-header elevated class="bg-primary text-white">
            <q-toolbar>
                <q-btn dense flat round icon="menu" @click="toggleLeftDrawer" />
                <q-toolbar-title>
                    LIQ Starter Kit
                </q-toolbar-title>
            </q-toolbar>
        </q-header>

        <q-drawer show-if-above v-model="leftDrawerOpen" side="left" bordered>
            <q-list>
                <q-item-label header>Menu Utama</q-item-label>

                <Link :href="route('dashboard')" as="div">
                    <q-item clickable v-ripple :active="route().current('dashboard')">
                        <q-item-section avatar>
                            <q-icon name="dashboard" />
                        </q-item-section>
                        <q-item-section>
                            Dashboard
                        </q-item-section>
                    </q-item>
                </Link>

                <Link :href="route('profile.edit')" as="div">
                    <q-item clickable v-ripple :active="route().current('profile.edit')">
                        <q-item-section avatar>
                            <q-icon name="person" />
                        </q-item-section>
                        <q-item-section>
                            Profil Saya
                        </q-item-section>
                    </q-item>
                </Link>

                <Link :href="route('logout')" method="post" as="div">
                    <q-item clickable v-ripple>
                        <q-item-section avatar>
                            <q-icon name="logout" />
                        </q-item-section>
                        <q-item-section>
                            Logout
                        </q-item-section>
                    </q-item>
                </Link>
            </q-list>
        </q-drawer>

        <q-page-container>
            <q-page padding>
                <slot />
            </q-page>
        </q-page-container>

    </q-layout>
</template>