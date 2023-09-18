<script setup lang="ts">
import { ref } from 'vue';
import type {Contact} from "@/App.vue";
const props = defineProps<{ contacts: Contact[]}>();
const emit = defineEmits(['sendContact']);
const addContactMessage = ref('');


function addContact() {

  let contact: Contact = {name: 'Eva', email: 'Eva@mockmail.com'};

  if (props.contacts.some(existingContact => existingContact.email === contact.email)) {
    addContactMessage.value = 'Contact already exists';
    return;
  }

  addContactMessage.value = 'You added a new contact';
  emit('sendContact', contact);
}
</script>

<template>
  <button @click="addContact">Add Contact</button>


  <div>{{ addContactMessage}}</div>

</template>





