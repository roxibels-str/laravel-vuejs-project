<script setup>
import { useForm } from '@inertiajs/vue3';

const form = useForm({
  name: '',
  company: '',
  phone: '',
  email: '',
});


function createContact() {
  if (confirm('Are you sure you want to create this contact?')) {
    form.post('/contacts', {
      preserveScroll: true,
      onSuccess: () => form.reset(),
    });
  }
}
</script>

<template>
        <!-- Modal for Create Contact -->
    <Modal :show="showCreateModal" @close="closeModal" class="modal-sm" >
        <div>
            <h1>Create Contact</h1>
            <form @submit.prevent="createContact">
            <div>
                <label for="name">Name:</label>
                <input type="text" v-model="form.name" id="name" required>
            </div>
            <div>
                <label for="company">Company:</label>
                <input type="text" v-model="form.company" id="company">
            </div>
            <div>
                <label for="phone">Phone:</label>
                <input type="text" v-model="form.phone" id="phone">
            </div>
            <div>
                <label for="email">Email:</label>
                <input type="email" v-model="form.email" id="email" required>
            </div>
            <button type="submit">Create</button>
            </form>
        </div>
    </Modal>
</template>
