<script setup>
defineOptions({
    name: "AuthLayout",
});
</script>

<template>
    <q-layout view="hHh lpR fff" class="bg-gradient">
        <q-header elevated class="bg-primary text-white">
            <q-toolbar style="max-width: 980px; margin: 0 auto">
                <q-toolbar-title align="center">
                    <q-img
                        src="/assets/img/favicon1.png"
                        style="
                            height: 32px;
                            max-width: 100%;
                            margin-right: 12px;
                            vertical-align: middle;
                        "
                        fit="contain"
                    />
                </q-toolbar-title>
            </q-toolbar>
        </q-header>
        <q-page-container style="max-width: 1024px; margin: 20px auto 0">
            <slot></slot>
        </q-page-container>
        <q-footer class="transparent">
            <div
                class="q-mt-lg q-mb-md justify-center items-center flex text-grey-6"
            >
                <span
                    >&copy; 2025 - {{ $config.APP_NAME }} v{{
                        $config.APP_VERSION_STR
                    }}</span
                >
            </div>
        </q-footer>
    </q-layout>
</template>

<style scoped>
.bg-gradient {
background: linear-gradient(135deg, #02d1d0, #034246);
min-height: 100vh;
}

.q-toolbar a {
color: #ddd;
text-decoration: none; 
}

.q-toolbar a:hover {
color: #fff;
}
</style>
