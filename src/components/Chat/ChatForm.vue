<script setup>
  import { ref, reactive } from 'vue';


  function doit(){
  }
</script>

<template>
  <div class="form">
    <div>
    <input v-model="newMessage.user" placeholder="Your name" />
    <input v-model="newMessage.text" placeholder="Your message" />
    <button @click="postMessage">Send</button>
  </div>
  </div>
</template>

<style scoped>

</style>
