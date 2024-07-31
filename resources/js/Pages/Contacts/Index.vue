<script setup>
import { ref } from 'vue';
import { usePage } from '@inertiajs/vue3';
import { Link } from '@inertiajs/vue3';
import AuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue';
import { Head } from '@inertiajs/vue3';


const { props } = usePage();
const contacts = ref(props.contacts);


</script>

<template>
    <Head title="Home" />
    <AuthenticatedLayout>


        <template #header>
            <h2 class="font-semibold text-xl text-gray-800 leading-tight">Contact List</h2>
        </template>
    <div>
        <Link href="/contacts/create" class="text-success">Create Contact</Link>
        <ul>
        <li v-for="contact in contacts" :key="contact.id">
            {{ contact.name }} - {{ contact.email }} - {{ contact.phone }} - {{ contact.company }}
            <Link :href="`/contacts/${contact.id}/edit`">Edit</Link>
        </li>
        </ul>


  </div>
</AuthenticatedLayout>
</template>


