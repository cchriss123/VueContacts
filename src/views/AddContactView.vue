<script setup lang="ts">
import AddContact from "@/components/AddContact.vue";
defineProps(['contacts']);
defineEmits(['sendContact']);
</script>

<template>

  <div><AddContact :contacts="contacts" @sendContact="contact => $emit('sendContact', contact)"/></div>
</template>

<style>
</style>
