<!-- ChatMessages.vue -->
<template>
  <h2>Messages</h2>
  <ul>
    <li v-for="(message, index) in messages" :key="index">
      <strong>{{ message.user }}</strong>: {{ message.text }}
    </li>
  </ul>
</template>

<script setup>
import { defineProps } from 'vue';

const props = defineProps(['messages']);
</script>

<style scoped>
/* Add any styles for your ChatMessages component here */
</style>
