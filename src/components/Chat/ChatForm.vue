<script setup>
  import { ref, reactive } from 'vue';

  function doit(){
    // comments.push({name: name.value, message: "Hello"});
  }
</script>

<template>
  <div class="form">
    <!-- <h3>{{ name }}</h3>
    <ul>
      <li v-for="comment in comments">
        <strong>{{ comment.name }}</strong>: {{ comment.message }}
      </li>
    </ul> -->

    <input  type="text" placeholder="Type your message here" />
    <button @click="doit">Send</button>
  </div>
</template>

<style scoped>

</style>
