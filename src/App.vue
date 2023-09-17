<script setup lang="ts">
import { RouterLink, RouterView } from 'vue-router'


export interface Contact {
  id: number;
  name: string;
  email: string;
}

const contacts: Contact[] = [
  { id: 1, name: 'John Doe' , email: 'John@mockmail.com'},
  { id: 2, name: 'Jane Doe' , email: 'Jane@mockmail.com'},
  { id: 3, name: 'Gunnar' , email: 'Gunnar@mockmail.com'},
];







</script>

<template>

  <h3>Contacts</h3>
  <div><RouterLink to="/">Home</RouterLink></div>
  <div><RouterLink to="/about">Add Contact</RouterLink></div>
  <div><RouterView :contacts="contacts"/></div>


</template>

<style scoped>

</style>
