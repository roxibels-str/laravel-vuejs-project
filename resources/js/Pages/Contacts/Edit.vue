<script setup>
import { ref } from 'vue';
import { usePage } from '@inertiajs/vue3';

const { props } = usePage();
const contact = ref(props.contact);

function updateContact() {
  Inertia.put(`/contacts/${contact.value.id}`, contact.value);
}
</script>

<template>
  <div>
    <h1>Edit Contact</h1>
    <form @submit.prevent="updateContact">
      <div>
        <label for="name">Name:</label>
        <input type="text" v-model="contact.name" id="name" required>
      </div>
      <div>
        <label for="company">Company:</label>
        <input type="text" v-model="contact.company" id="company">
      </div>
      <div>
        <label for="phone">Phone:</label>
        <input type="text" v-model="contact.phone" id="phone">
      </div>
      <div>
        <label for="email">Email:</label>
        <input type="email" v-model="contact.email" id="email" required>
      </div>
      <button type="submit">Update</button>
    </form>
  </div>
</template>
