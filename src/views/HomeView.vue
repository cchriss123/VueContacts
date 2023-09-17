<script setup lang="ts">
import ShowContacts from "@/components/ShowContacts.vue";

defineProps(['contacts']);
</script>

<template>
  <h3>Home View</h3>
  <div><ShowContacts :contacts="contacts"/></div>
</template>
