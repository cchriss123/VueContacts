<script setup lang="ts">
import { RouterLink, RouterView } from 'vue-router'

</script>

<template>

  <h3>Contacts</h3>
  <div><RouterLink to="/">Home</RouterLink></div>
  <div><RouterLink to="/about">Reg</RouterLink></div>


  <h3>Router View</h3>
  <div><RouterView/></div>






</template>

<style scoped>

</style>
