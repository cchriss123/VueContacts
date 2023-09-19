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

  addContactMessage.value = `${contact.value.name} was added to your contacts`;
  emit('sendContact', contact.value);
  contact = ref<Contact>({ name: '', email: '' , date: new Date()});
}
</script>

<template>
  <div class="content-container">
  <form @submit.prevent="addContact">
    <label for="name">Name</label>
    <input v-model="contact.name" placeholder="Enter name" type="text" required>
    <label for="email">Email</label>
    <input v-model="contact.email" placeholder="Enter email" type="email" required>

    <button type="submit">Add Contact</button>
  </form>
    <div class="add-message" v-if="addContactMessage">{{ addContactMessage}}</div>
  </div>
</template>

<style scoped>

.content-container {
  width: 95%;
  display: flex;
  margin-top: 20px;
  margin-left: auto;
  margin-right: auto;


}

form {
  display: flex;
  flex-wrap: wrap;
  padding: 20px;
  background-color: rgb(53, 53, 53);
  border-radius: 10px;
  margin-top: 20px;
}

.add-message {
  margin-top: 20px;
  color: white;
  font-size: 20px;
  padding: 10px 20px;
  background-color: rgb(53, 53, 53);
  border-radius: 10px;
}

input[type="text"],
input[type="email"] {
  width: 100%;
  height: 30px;
  background-color: rgb(36, 36, 36);
  border-radius: 8px;
  color: white;
  font-size: 16px;
  margin-bottom: 20px;
}

button[type="submit"]  {
  color: white;
  background-color: rgb(53, 53, 53);
  border-radius: 30px;
  border: 2px solid rgb(73, 73, 73);
  border-right-color: rgb(36, 36, 36);
  border-bottom-color: rgb(36, 36, 36);
  font-size: 14px;
  padding: 6px 30px;
  text-decoration: none;
  margin-left: auto;
  margin-right: auto;

}
button[type="submit"]:hover {
  background-color: rgb(73, 73, 73);
}

@media screen and (min-width: 600px) {
  .content-container {
    width: 500px;
  }
}
</style>
