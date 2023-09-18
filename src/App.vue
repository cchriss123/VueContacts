<script setup lang="ts">
import { RouterLink, RouterView } from 'vue-router'
import AddContactView from "@/views/AddContactView.vue";





export interface Contact {
  name: string;
  email: string;
}

const contacts: Contact[] = [
  { name: 'John Doe' , email: 'John@mockmail.com'},
  { name: 'Jane Doe' , email: 'Jane@mockmail.com'},
  { name: 'Gunnar' , email: 'Gunnar@mockmail.com'},
];


const emit = defineEmits(['sendContact']);

function addNewContact(newContact: Contact) {
  contacts.push(newContact);
  console.log(contacts);
}

</script>

<template>

  <h3>Contacts</h3>
  <div><RouterLink to="/">Home</RouterLink></div>
  <div><RouterLink to="/about">Add Contact</RouterLink></div>
  <RouterView :contacts="contacts" @sendContact="addNewContact"/>

</template>

<style scoped>

</style>
