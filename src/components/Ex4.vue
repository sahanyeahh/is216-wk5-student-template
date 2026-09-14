<script setup>
import { ref } from 'vue'
const items = ref(['keyboard', 'mouse', 'iPhone', 'macbook', 'adapter'])

// TODO: Add Code Here
const newItem = ref('')

function deleteItem(index) {
  items.value.splice(index, 1)
}

function addItem() {
  if (newItem.value.trim() !== '') {
    items.value.push(newItem.value)
    newItem.value = ''   // clear the text box after adding
  }
}

</script>

<template>

    <h2>Shopping Cart</h2>
    <!-- TODO: Add Code Here -->
    <ul>
      <li v-for="(item, index) in items" :key="index">
        {{ item }}
        <button @click="deleteItem(index)">Delete!</button>
      </li>
    </ul>

    <input v-model="newItem" @keyup.enter="addItem" />
    <button @click="addItem">Add!</button>
   
</template>
