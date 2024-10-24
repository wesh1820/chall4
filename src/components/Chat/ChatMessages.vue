<!-- ChatMessages.vue -->
<script setup>
import { defineProps, onMounted, reactive } from 'vue';

const props = defineProps(['messages']); // Accept messages as a prop

onMounted(() => {
  fetch('https://challenge4-9b1t.onrender.com/api/v1/messages')
    .then(response => response.json())
    .then(data => {
      data.data.messages.forEach(message => {
        props.messages.push(message); // Push existing messages into the reactive array
      });
    });
});
</script>

<template>
  <h2>Comments</h2>
  <ul>
    <li v-for="(message, index) in messages" :key="index">
      <strong>{{ message.user }}</strong>: {{ message.text }}
    </li>
  </ul>
</template>

<style scoped>
/* Add any styles for your ChatMessages component here */
</style>
