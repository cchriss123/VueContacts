<script setup lang="ts">
import { RouterLink, RouterView } from 'vue-router'
import {ref} from "vue";
defineEmits(['sendContact', 'deleteContact']);

export interface Contact {
  name: string;
  email: string;
  number: string;
  date: Date;
}

const contacts = ref<Contact[]>([
  { name: 'Jesper' , email: 'Jesper@mockmail.com' , number: '0701234567' , date: new Date()},
  { name: 'John' , email: 'John@mockmail.com' , number: '0731234567' , date: new Date()},
  { name: 'Sara' , email: 'Sara@gmail.com' , number: '0761234567' , date: new Date()},
  { name: 'Anna' , email: 'Anna@mockmail.com' , number: '0706456546' , date: new Date()},
  { name: 'Gunnar' , email: 'Gunnar@hotmail.com' , number: '0701234567' , date: new Date()}]);

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
      <div class="add"><RouterLink to="/add">Add </RouterLink></div>
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
  justify-content:space-between;
  //border: white solid 2px;


}

.home a, .add a {
  color: white;
  border-radius: 30px;
  background-color: rgb(30, 30, 90);
  border: 2px solid rgb(50, 50, 150);
  border-right-color: rgb(15, 15, 45);
  border-bottom-color: rgb(15, 15, 45);
  font-size: 14px;
  padding: 6px 30px;
  text-decoration: none;
}
.home a:hover, .add a:hover {
  background-color: rgb(50, 50, 150);
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
    text-align: left;
  }
  .topContainer{
    width: 95%;
  }
  .topContainer-outer{
    display: flex;
    justify-content: center;
  }


  .add{
    text-align: right;
  }
}

@media screen and (min-width: 1000px) {
  .topContainer{
    width: 60%;
  }
}
</style>
