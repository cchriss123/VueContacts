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
  <div class="content-container">
    <button class="sort" @click="toggleSorting">{{ isSortedByName ? "Sort by Most Recent" : "Sort by Name" }}</button>
    <div v-for="(contact, i) in sortedList()" :key="i">
      <div>{{ contact.name }}, {{ contact.email }}, {{ formatDate(contact.date) }}</div>
      <div><button @click="$emit('deleteContact', contact.email)">Delete</button></div>
    </div>
  </div>
</template>


<style scoped>

.content-container {
  width: 95%;
  display: flex;
  flex-direction: column;
  margin-top: 20px;
  margin-left: auto;
  margin-right: auto;
}

.sort {
  color: white;
  background-color: rgb(53, 53, 53);
  border-radius: 30px;
  border: 2px solid rgb(73, 73, 73);
  border-right-color: rgb(36, 36, 36);
  border-bottom-color: rgb(36, 36, 36);
  font-size: 14px;
  padding: 6px 30px;
  text-decoration: none;
  margin-right: auto;
  margin-top: 20px;
  margin-bottom: 20px;
}





@media screen and (min-width: 1000px) {
  .content-container{
    width: 60%;
  }

}




</style>