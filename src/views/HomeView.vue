<script setup lang="ts">
import ShowContacts from "@/components/ShowContacts.vue";
const emit = defineEmits(['deleteContact']);
defineProps(['contacts']);
</script>

<template>

  <div><ShowContacts :contacts="contacts" @deleteContact="contact => emit('deleteContact', contact)"/></div>
</template>
