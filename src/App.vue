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
  <div class="topContainer-outer">
    <div class="topContainer">
      <div class="header-outer"><h1>Contacts</h1></div>
      <div class="home"><RouterLink to="/">Home</RouterLink></div>
      <div class="add"><RouterLink to="/about">Add </RouterLink></div>
    </div>
  </div>

  <RouterView :contacts="contacts" @sendContact="addNewContact" @deleteContact="deleteContact"/>
</template>

<style scoped>

.topContainer-outer{
  border-bottom: white solid 2px;
}

.topContainer {
  height: 150px;
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
}

.home a, .add a {
  color: white;
  background-color: rgb(53, 53, 53);
  border-radius: 30px;
  border: 2px solid rgb(73, 73, 73);
  border-right-color: rgb(36, 36, 36);
  border-bottom-color: rgb(36, 36, 36);
  font-size: 14px;
  padding: 6px 30px;
  text-decoration: none;
}
.home a:hover, .add a:hover {
  background-color: rgb(73, 73, 73);
}


.header-outer{
  width: 100%;
  text-align: center;
}

.home, .add{
  width: 50%;
  margin-top: 20px;
  margin-bottom: 20px;
  box-sizing: border-box;
  text-align: center;
}

@media screen and (min-width: 600px) {
  .home, .add, .header-outer{
    width: 33%;
    margin-top: auto;
  }
  .home{
    order: -1;
  }
}

@media screen and (min-width: 1000px) {
  .topContainer{
    width: 60%;
  }
  .topContainer-outer{
    display: flex;
    justify-content: center;

  }
}
</style>
