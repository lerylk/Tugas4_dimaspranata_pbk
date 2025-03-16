<script setup>
import { ref } from 'vue';

const message = ref('Dimas')

//form binding
const inputText = ref('');  

//event listener
const count = ref(0);
const increment = () => count.value++;

//atribut binding
const changeColor = () => isClicked.value = !isClicked.value;

//conditional rendering
const toggleAwesome = () => isAwesome.value = !isAwesome.value;

const isAwesome = ref(true);
const isClicked = ref(false);
</script>

<template>
  <div>
    <h1>{{ message }}</h1>

    <input v-model="inputText" placeholder="Type something" />
    <p>You typed: {{ inputText }}</p>

   
    <h1>Count: {{ count }}</h1>
    <button @click="increment">Tambah Count</button>

    
    <h1 :class="isClicked ? 'title-clicked' : 'title'">Make me red or blue</h1>
    <button @click="changeColor">Change Color</button>


 
    <button @click="toggleAwesome">Toggle</button>
    <h1 v-if="isAwesome">Vue is awesome!</h1>
    <h1 v-else>Oh no </h1>

  </div>
</template>

<style>
.title { color: red; }
.title-clicked { color: blue; }
</style>