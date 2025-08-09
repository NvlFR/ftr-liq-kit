<script setup>
import { QLayout, QPageContainer, QPage } from 'quasar';
</script>

<template>
    <q-layout>
        <q-page-container>
            <q-page class="flex flex-center bg-grey-2">
                <div style="width: 400px; max-width: 90vw;">
                    <slot />
                </div>
            </q-page>
        </q-page-container>
    </q-layout>
</template>

<style scoped>
.flex-center {
    display: flex;
    justify-content: center;
    align-items: center;
}
</style>