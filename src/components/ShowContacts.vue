<script setup lang="ts">
import type {Contact} from "@/App.vue";
import {ref} from "vue";
const props = defineProps<{ contacts: Contact[]}>();
const emit = defineEmits(['deleteContact']);
let isSortedByName = ref(true);

// consider to use computed instead
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
  <button @click="toggleSorting">{{ isSortedByName ? "Sort by Most Recent" : "Sort by Name" }}</button>
  <div v-for="(contact, i) in sortedList()" :key="i">
    <div>{{ contact.name }}, {{ contact.email }}, {{ formatDate(contact.date) }}</div>
    <div><button @click="() => emit('deleteContact', contact.email)">Delete</button></div>
  </div>
</template>
