<script setup>
import { useForm } from '@inertiajs/vue3';
import { useQuasar } from 'quasar';

const $q = useQuasar();

const form = useForm({
    password: '',
});

const confirmUserDeletion = () => {
    $q.dialog({
        title: 'Apakah Anda yakin?',
        message: 'Setelah akun Anda dihapus, semua sumber daya dan datanya akan dihapus secara permanen. Silakan masukkan kata sandi Anda untuk mengonfirmasi bahwa Anda ingin menghapus akun Anda secara permanen.',
        prompt: {
            model: '',
            type: 'password',
            label: 'Password'
        },
        cancel: true,
        persistent: true,
        ok: {
            label: 'Hapus Akun',
            color: 'negative'
        }
    }).onOk(password => {
        form.password = password;
        form.delete(route('profile.destroy'));
    });
};
</script>

<template>
    <q-card>
        <q-card-section>
            <div class="text-h6">Hapus Akun</div>
            <div class="text-subtitle2">Setelah akun Anda dihapus, semua sumber daya dan datanya akan dihapus secara permanen.</div>
        </q-card-section>

        <q-card-section>
             <q-btn label="Hapus Akun Saya" color="negative" @click="confirmUserDeletion" />
        </q-card-section>
    </q-card>
</template>