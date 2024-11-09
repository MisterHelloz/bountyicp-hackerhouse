<script setup>
import { ref } from 'vue';
import { hello_world_backend } from 'declarations/hello_world_backend/index';
let greeting = ref('');
let submittedNames = ref([]);

async function handleSubmit(e) {
  e.preventDefault();
  const target = e.target;
  const name = target.querySelector('#name').value;
  await hello_world_backend.greet(name).then((response) => {
    greeting.value = response;
  });
}

async function handleShowNames() {
  submittedNames.value = await hello_world_backend.getSubmittedNames();
}
</script>

<template>
  <main>
    <img src="/logo2.svg" alt="DFINITY logo" />
    <br />
    <br />
    <form action="#" @submit="handleSubmit" class="form-container">
      <label for="name">Enter your name: &nbsp;</label>
      <input id="name" alt="Name" type="text" />
      <button type="submit" class="submit-button">Click Me!</button>
    </form>
    
    <button @click="handleShowNames" class="show-names-button">Show Submitted Names</button>
    
    <section id="greeting">{{ greeting }}</section>
    <section v-if="submittedNames.length > 0">
      <h3>Submitted Names:</h3>
      <ul>
        <li v-for="(name, index) in submittedNames" :key="index">{{ name }}</li>
      </ul>
    </section>
  </main>
</template>

<style scoped>
/* Center the content */
main {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  min-height: 100vh;
  text-align: center;
  background-color: #f7f7f7;
}

/* Form styling */
.form-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-bottom: 20px;
}

input[type="text"] {
  padding: 10px;
  margin: 10px;
  border-radius: 5px;
  border: 1px solid #ccc;
}

.submit-button {
  padding: 10px 20px;
  background-color: #007BFF;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  font-size: 16px;
  transition: background-color 0.3s ease;
}

.submit-button:hover {
  background-color: #0056b3;
}

.show-names-button {
  padding: 10px 20px;
  background-color: #28a745;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  font-size: 16px;
  transition: background-color 0.3s ease;
  margin-top: 20px;
}

.show-names-button:hover {
  background-color: #218838;
}

/* Styling for the greeting */
#greeting {
  font-size: 20px;
  font-weight: bold;
  margin-top: 20px;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  padding: 5px;
  font-size: 16px;
}
</style>
