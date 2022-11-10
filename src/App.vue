<script setup>
 import { ref } from "vue";

 const showModal = ref(false)
 const newNote = ref("")
 const notes = ref([])

 function getRandomColor() {
  return "hsl(" + Math.random() * 360 + ", 100%, 75%)";
 }

 const addNote = () => {
  notes.value.push({
    id: Math.floor(Math.random() * 10000),
    text: newNote.value,
    date:new Date(),
    bgColor: getRandomColor()
  })
    showModal.value = false
    newNote.value = ""
 }
</script>

<template>
  <main>
    <div class="overlay" v-if="showModal">
      <div class="modal">
        <textarea v-model="newNote" name="note" id="note" cols="30" rows="10"></textarea>
        <button @click="addNote">Add Note</button>
        <button class="close" @click="showModal=false">Close</button>
      </div>
    </div>
    <div class="container">
      <header>
        <h1>Notes</h1>
        <button @click="showModal=true">+</button>
      </header>
      <div class="cards-container">
        <div v-for="note in notes" :key="note.id" class="card" :style="{backgroundColor: note.bgColor}">
          <p class="main-text">{{ note.text }}</p>
          <p class="date">{{ note.date.toLocaleDateString("sr-RS") }}</p>
        </div>
      </div>
    </div>
  </main>
</template>

<style scoped> 
  main {
    height: 100vh;
    width: 100vw;
  }
  .container {
    max-width: 1000px;
    padding: 10px;
    margin: 0 auto;
  }
  header {
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
  h1 {
    font-weight: bold;
    font-size: 75px;
    margin-bottom: 25px;
  }
  header button {
    border: none;
    padding: 10px;
    width: 50px;
    height: 50px;
    cursor: pointer;
    background-color: rgb(40, 230, 40);
    border-radius: 100%;
    font-size: 20px;
  }
  .card {
    width: 225px;
    height: 225px;
    background-color: rgb(237, 182, 44);
    padding: 10px;
    border-radius: 15px;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    margin-right: 20px;
    margin-bottom: 20px;
  }
  .main-text, .date {
    color: black;
  }
  .date {
    font-size: 12.5px;
    font-weight: bold;
  }
  .cards-container {
    display: flex;
    flex-wrap: wrap;
  }
  .overlay {
    position: absolute;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.77);
    z-index: 10;
    display: flex;
    align-items: center;
    justify-content: center;

  }
  .modal {
    width: 750px;
    background-color: var(--vt-c-black-soft);
    border-radius: 10px;
    padding: 30px;
    position: relative;
    display: flex;
    flex-direction: column;
  }
  .modal button {
    padding: 10px 20px;
    font-size: 20px;
    width: 100%;
    background-color: blueviolet;
    border: none;
    color: white;
    cursor: pointer;
    margin-top: 15px;
  }
  .modal .close {
    background-color: rgb(193, 15, 15);
    margin-top: 7px;
  }
  .modal textarea {
    background-color: var(--vt-c-text-light-2);
    resize: none;
    color: white;
    font-size: 15px;
  }
</style>