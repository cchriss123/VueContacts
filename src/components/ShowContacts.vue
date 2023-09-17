<script setup lang="ts">
import type {Contact} from "@/App.vue";

const props = defineProps<{ contacts: Contact[]}>();


</script>





<template>
  <div v-for="contact in props.contacts" :key="contact.id">
    <div>{{ contact.name }}, {{ contact.email }}</div>
  </div>
</template>
