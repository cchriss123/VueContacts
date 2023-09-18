<script setup lang="ts">
import { ref } from 'vue';
import type {Contact} from "@/App.vue";
const props = defineProps<{ contacts: Contact[]}>();
const emit = defineEmits(['sendContact']);
const addContactMessage = ref('');

let contact = ref<Contact>({ name: '', email: '' , date: new Date()});

function addContact() {

  if (props.contacts.some(existingContact => existingContact.email === contact.value.email)) {
    addContactMessage.value = 'Contact already exists';
    return;
  }

  addContactMessage.value = 'You added a new contact';
  emit('sendContact', contact.value);
}
</script>

<template>
  <form @submit.prevent="addContact">
    <input v-model="contact.name" placeholder="Enter name" required>
    <input v-model="contact.email" placeholder="Enter email" type="email" required>
    <button type="submit">Add Contact</button>
  </form>
  <div>{{ addContactMessage}}</div>
</template>
