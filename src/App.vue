<script setup lang="ts">
import { RouterLink, RouterView } from 'vue-router'
import {ref} from "vue";
defineEmits(['sendContact', 'deleteContact']);

export interface Contact {
  name: string;
  email: string;
  date: Date;
}

const contacts = ref<Contact[]>([
  { name: 'Jesper' , email: 'John@mockmail.com' , date: new Date()},
  { name: 'Anna' , email: 'Anna@mockmail.com' , date: new Date()},
  { name: 'Gunnar' , email: 'Gunnar@mockmail.com' , date: new Date()},
]);

function addNewContact(newContact: Contact) {
  contacts.value.push(newContact);
}

function deleteContact(email: string) {
  contacts.value = contacts.value.filter(existingContact => existingContact.email !== email);
}




</script>

<template>
  <h3>Contacts</h3>
  <div><RouterLink to="/">Home</RouterLink></div>
  <div><RouterLink to="/about">Add Contact</RouterLink></div>
  <RouterView :contacts="contacts" @sendContact="addNewContact" @deleteContact="deleteContact"/>
</template>

<style scoped>

</style>
