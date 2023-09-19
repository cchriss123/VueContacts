<script setup lang="ts">
import AddContact from "@/components/AddContact.vue";
defineProps(['contacts']);
defineEmits(['sendContact']);
</script>

<template>
  <h3>Add contact View</h3>
  <div><AddContact :contacts="contacts" @sendContact="contact => $emit('sendContact', contact)"/></div>
</template>

<style>
</style>
