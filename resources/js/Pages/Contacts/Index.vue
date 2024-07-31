<script setup>
import { ref } from 'vue';
import { usePage, useForm } from '@inertiajs/vue3';
import { Link } from '@inertiajs/vue3';
import AuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue';
import { Head } from '@inertiajs/vue3';
import PrimaryButton from '@/Components/PrimaryButton.vue';
import DangerButton from '@/Components/DangerButton.vue';
import SecondaryButton from '@/Components/SecondaryButton.vue';
import Modal from '@/Components/Modal.vue';

import InputError from '@/Components/InputError.vue';
import InputLabel from '@/Components/InputLabel.vue';
import TextInput from '@/Components/TextInput.vue';

const { props } = usePage();
const contacts = ref(props.contacts);

const form = useForm({
    name: '',
    company: '',
    phone: '',
    email: '',
});
const showDeletionModal = ref(false);
const showCreationModal = ref(false);
const selectedContactId = ref(null);

// Delete Method Modal
const confirmContactDeletion = (id) => {
    selectedContactId.value = id;
    showDeletionModal.value = true;
};

const deleteContact = () => {
    form.delete(route('contact.destroy', selectedContactId.value), {
        preserveScroll: true,
        onSuccess: () => closeModal(),
        onFinish: () => form.reset(),
    });
};

const openContactCreation = () => {
    showCreationModal.value = true;
};

const createContact = () => {
    if (confirm('Are you sure you want to create this contact?')) {
        form.post('/contacts', {
            preserveScroll: true,
            onSuccess: () => closeModal(),
        });
    }
};

const closeModal = () => {
    showDeletionModal.value = false;
    showCreationModal.value = false;
    selectedContactId.value = null;
    form.reset();
};
</script>

<template>
    <Head title="Contacts" />
    <AuthenticatedLayout>
        <template #header>
            <h2 class="font-semibold text-xl text-gray-800 leading-tight">Contact List</h2>
        </template>
        <div class="py-3">
            <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
                <PrimaryButton class="my-3" @click="openContactCreation">Create Contact</PrimaryButton>
                <div class="bg-white overflow-hidden shadow-sm sm:rounded-lg">
                    <div class="card">
                        <div class="card-header">
                            <!-- Contact List Table -->
                            <table class="table table-bordered table-striped table-hover">
                                <thead>
                                    <tr>
                                        <th>Name</th>
                                        <th>Company</th>
                                        <th>Phone</th>
                                        <th>Email</th>
                                        <th colspan="3">Actions</th>
                                    </tr>
                                </thead>
                                <tbody>
                                    <tr v-for="contact in contacts" :key="contact.id">
                                        <td>{{ contact.name }}</td>
                                        <td>{{ contact.company }}</td>
                                        <td>{{ contact.phone }}</td>
                                        <td>{{ contact.email }}</td>
                                        <td>
                                            <Link :href="`/contacts/${contact.id}/edit`" class="btn btn-outline-secondary">Edit</Link>
                                        </td>
                                        <td>
                                            <Link :href="`/contacts/${contact.id}/edit`" class="btn btn-outline-secondary">View</Link>
                                        </td>
                                        <td>
                                            <DangerButton @click="() => confirmContactDeletion(contact.id)">Delete</DangerButton>
                                        </td>
                                    </tr>
                                </tbody>
                            </table>

                            <!-- Modal for Delete Contact -->
                            <Modal :show="showDeletionModal" @close="closeModal">
                                <div class="p-6">
                                    <h2 class="m-3">
                                        Are you sure you want to delete this contact?
                                    </h2>
                                    <div class="mt-6 flex justify-end p-3">
                                        <DangerButton @click="deleteContact" class="mx-3">Delete Contact</DangerButton>
                                        <SecondaryButton @click="closeModal">Cancel</SecondaryButton>
                                    </div>
                                </div>
                            </Modal>

                            <!-- Modal for Create Contact -->
                            <Modal :show="showCreationModal" @close="closeModal">
                                <div class="p-6">
                                    <div class="modal-dialog">
                                        <div class="modal-content">
                                            <div class="modal-header">
                                                <h1 class="modal-title fs-5" id="">Create Contact</h1>
                                                <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close" @click="closeModal"></button>
                                            </div>
                                            <div class="modal-body">
                                                <form @submit.prevent="createContact" class="">

                                                <div class="">
                                                    <InputLabel for="name" value="Name" />
                                                    <TextInput type="text" v-model="form.name" id="name" required/>
                                                </div>
                                                <div class="">
                                                    <InputLabel for="company" value="Company" />
                                                    <TextInput type="text" v-model="form.company" id="company"/>
                                                </div>
                                                <div class="">
                                                    <InputLabel for="phone" value="Phone" />
                                                    <TextInput type="text" v-model="form.phone" id="phone"/>
                                                </div>
                                                <div class="">
                                                    <InputLabel for="email" value="Email" />
                                                    <TextInput type="email" v-model="form.email" id="email" required/>
                                                </div>
                                                <div class="">
                                                    <PrimaryButton type="submit" class="my-3">Create Contact</PrimaryButton>
                                                </div>
                                            </form>
                                            </div>
                                            <div class="modal-footer">
                                            </div>
                                        </div>
                                    </div>
                                </div>
                            </Modal>

                        </div>
                    </div>
                </div>
            </div>
        </div>
    </AuthenticatedLayout>
</template>
