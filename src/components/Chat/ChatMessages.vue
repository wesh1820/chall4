<script setup>
import { defineProps } from 'vue';
const props = defineProps({
  messages: Array
});
</script>

<template>
  <h2>Comments</h2>
  <ul>
    <li v-for="message in messages" :key="message.timestamp">
      <strong>{{ message.user }}</strong>: {{ message.text }}
    </li>
  </ul>
</template>

<style scoped>
/* Voeg styling toe indien nodig */
</style>
