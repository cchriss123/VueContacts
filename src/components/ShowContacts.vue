<script setup lang="ts">
import type {Contact} from "@/App.vue";
import {ref} from "vue";
const props = defineProps<{ contacts: Contact[]}>();
defineEmits(['deleteContact']);
let isSortedByName = ref(true);

function sortedList() {
  const contactsCopy = [...props.contacts];
  if (isSortedByName.value)
    return contactsCopy.sort((a, b) => a.name.localeCompare(b.name));

  return contactsCopy.reverse()
}

function formatDate(dateString) {
  const date = new Date(dateString);
  return `${date.toLocaleDateString()}`;
}

function toggleSorting() {
  isSortedByName.value = !isSortedByName.value;
}

</script>

<template>
  <div class="form-container">
    <div class="sort-container">
      <button class="sort" @click="toggleSorting">{{ isSortedByName ? "Sorted by name" : "Sorted by date" }}</button>
    </div>
    <div class="info-container" v-for="(contact, i) in sortedList()" :key="i">
      <div>Name: {{ contact.name }}</div>
      <div>Email: {{ contact.email }}</div>
      <div>Number: {{ contact.number }}</div>
      <div>Date added: {{ formatDate(contact.date)}}</div>
      <button class="delete" @click="$emit('deleteContact', contact.email)">Delete</button>
    </div>
  </div>
</template>


<style scoped>

.form-container {
  width: 95%;
  display: flex;
  flex-wrap: wrap;
  gap: 10px;
  margin: 20px auto 40px;

}

.sort {
  color: white;
  border-radius: 30px;
  background-color: rgb(30, 30, 90);
  border: 2px solid rgb(50, 50, 150);
  border-right-color: rgb(15, 15, 45);
  border-bottom-color: rgb(15, 15, 45);
  font-size: 14px;
  padding: 6px 30px;
  text-decoration: none;
  margin: 20px auto;
}

.sort:hover, .delete:hover {
  background-color: rgb(50, 50, 150);
}

.sort-container {
  width: 100%;
  display: flex;
  justify-content: center;
  margin-bottom: 10px;

}

.info-container{
  box-sizing: border-box;
  padding: 15px;
  font-size: 14px;
  color: white;
  width: calc(100%);
  background-color: rgb(25,25,75);
  border-radius: 10px;
  display: flex;
  flex-direction: column;
  gap: 10px;
  overflow: hidden;
}
.info-container > div {
  display: flex;
  flex-direction: column;
  //overflow-wrap: break-word;
}


.delete{
  color: white;

  border-radius: 30px;
  background-color: rgb(30, 30, 90);
  border: 2px solid rgb(50, 50, 150);
  border-right-color: rgb(15, 15, 45);
  border-bottom-color: rgb(15, 15, 45);
  font-size: 14px;
  padding: 6px 30px;
  margin-left: auto;
}




@media screen and (min-width: 600px) {
  .sort {
    margin-right: auto;
    margin-left: 0;
  }
  .info-container{
    width: calc(50% - 5px);
  }
}

@media screen and (min-width: 1000px) {
  .form-container{
    width: 60%;
  }
}

@media screen and (min-width: 1300px) {
  .info-container{
    width: calc(33% - 5px);
  }
}
</style>