<script setup>
import AuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue';
import { Head } from '@inertiajs/vue3';
import { Link } from '@inertiajs/vue3';
</script>

<template>
    <Head title="Dashboard" />

    <AuthenticatedLayout>
        <template #header>
            <h2 class="font-semibold text-xl text-gray-800 leading-tight">Dashboard</h2>
        </template>

        <div class="py-2">
            <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
                <div class="bg-white overflow-hidden shadow-sm sm:rounded-lg">
                    <div class="p-6 text-gray-900">You're logged in!</div>
                </div>
            </div>
        </div>

        <div class="max-w-7xl mx-auto sm:px-6 lg:px-8 py-3">
            <div class="row align-items-md-stretch bg-gray">
            <div class="col-md-6 ">
                <div class="h-100 p-5 bg-gray-200 border rounded-3 bg-gray overflow-hidden shadow-sm sm:rounded-lg">
                <h2 class="font-bold text-xl text-white-800 leading-tight">Contact Management</h2>
                <p class="fs-s py-4">This is a long sentence.</p>
                <Link :href="`/contacts`"><button class="btn btn-outline-secondary" type="button">Manage Contacts</button></Link>
                </div>
            </div>
            </div>
        </div>

    </AuthenticatedLayout>
</template>
