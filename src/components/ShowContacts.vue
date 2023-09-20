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
      <button class="sort" @click="toggleSorting">{{ isSortedByName ? "Sort by Most Recent" : "Sort by Name" }}</button>
    </div>
    <div class="info-container" v-for="(contact, i) in sortedList()" :key="i">
      <div>{{ contact.name }}</div>
      <div>{{ contact.email }}</div>
      <div>{{ formatDate(contact.date)}}</div>
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
  background-color: rgb(53, 53, 53);
  border-radius: 30px;
  border: 2px solid rgb(73, 73, 73);
  border-right-color: rgb(36, 36, 36);
  border-bottom-color: rgb(36, 36, 36);
  font-size: 14px;
  padding: 6px 30px;
  text-decoration: none;
  margin: 20px auto;
}

.sort:hover, .delete:hover {
  background-color: rgb(73, 73, 73);
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
  background-color: rgb(36,36,36);
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
  background-color: rgb(53, 53, 53);
  border-radius: 30px;
  border: 2px solid rgb(73, 73, 73);
  border-right-color: rgb(36, 36, 36);
  border-bottom-color: rgb(36, 36, 36);
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
    width: calc(33% - 5px);
  }
}





@media screen and (min-width: 1000px) {
  .form-container{
    width: 60%;
  }
  .info-container{
    width: calc(33% - 5px);
  }

}
</style>