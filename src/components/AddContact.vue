<script setup lang="ts">
import { ref } from 'vue';
import type {Contact} from "@/App.vue";
const props = defineProps<{ contacts: Contact[]}>();
const emit = defineEmits(['sendContact']);
const addContactMessage = ref('');

let contact = ref<Contact>({ name: '', email: '' , number: '', date: new Date()});

function addContact() {

  if (props.contacts.some(existingContact => existingContact.email === contact.value.email)) {
    addContactMessage.value = 'Contact already exists';
    return;
  }

  addContactMessage.value = `${contact.value.name} was added to your contacts`;
  emit('sendContact', contact.value);
  contact = ref<Contact>({ name: '', email: '' , number: '', date: new Date()});
}
</script>

<template>
  <div class=" content-container">

    <div class="form-container">
    <form @submit.prevent="addContact">
      <label for="name">Name</label>
      <input v-model="contact.name" placeholder="Enter name" type="text" required>
      <label for="email">Email</label>
      <input v-model="contact.email" placeholder="Enter email" type="email" required>
      <label for="number">Number</label>
      <input v-model="contact.number" placeholder="Enter number" type="text" pattern="\d{3,}" maxlength="18" required>


      <button type="submit">Add Contact</button>
    </form>
    </div>
    <div class="picture-container"><img src="../assets/mailbox.jpg" alt="mailbox"></div>
    <div class="add-message" v-if="addContactMessage">{{ addContactMessage}}</div>


  </div>
</template>

<style scoped>

.content-container {
  display: flex;
  justify-content: space-between;
  flex-wrap: wrap;

}

.form-container,
.picture-container{
  width: 95%;
  display: flex;
  margin-top: 20px;
  margin-left: auto;
  margin-right: auto;
  box-sizing: border-box;



}

.picture-container {
  display: none;
  border-radius: 10px;

}

form {

  display: flex;

  flex-wrap: wrap;

  padding: 20px;
  background-color: rgb(25, 25, 75);
  border-radius: 10px;


}

.add-message {
  margin-top: 20px;
  margin-left: 2.5%;

  color: white;
  font-size: 20px;
  padding: 10px 20px;
  background-color: rgb(25, 25, 75);
  border-radius: 10px;




}

input[type="text"],
input[type="email"] {
  width: 100%;
  height: 30px;
  background-color: rgb(10, 10, 30);
  border-radius: 10px;
  color: white;
  font-size: 16px;
  margin-bottom: 20px;


}

button[type="submit"]  {
  color: white;

  border-radius: 30px;
  background-color: rgb(30, 30, 90);
  border: 2px solid rgb(50, 50, 150);
  border-right-color: rgb(15, 15, 45);
  border-bottom-color: rgb(15, 15, 45);

  font-size: 14px;
  padding: 6px 30px;
  text-decoration: none;
  margin-left: auto;
  margin-right: auto;
  height: 36px;
}
button[type="submit"]:hover {
  background-color: rgb(50, 50, 150);
}

@media screen and (min-width: 600px) {
  .form-container,
  .picture-container{
    width: calc(50% - 5px);
    margin-left: 0;
    height: 300px;
  }
  .content-container{
    width: 95%;
    margin-right: auto;
    margin-left: auto;
    gap: 10px;
  }

  .picture-container {
    display: block;
    overflow: hidden;
  }

  .picture-container img {
    width: 100%;
    height: 100%;
    object-fit: cover;
  }

  .add-message {
    margin-left: 0;
  }

  @media screen and (min-width: 1000px) {
    .content-container{
      width: 60%;
    }
  }
}
</style>
