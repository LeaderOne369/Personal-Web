<script setup lang="ts">
import { ref } from 'vue'

const messageVal = ref<string>('')
const messageList = ref<Array<string>>([])
const sendMessage = () => {
  messageList.value.push(messageVal.value)
  sessionStorage.setItem('message', JSON.stringify(messageList.value))
  sessionStorage.setItem('status', true)
  messageVal.value = ''
}
</script>

<template>
  <div>
    <input
      v-model="messageVal"
      class="message"
      type="text"
    >
    <button
      class="default"
      @click="sendMessage"
    >
      发送
    </button>
  </div>
</template>

<style scoped>
input {
  box-sizing: border-box;
  padding: 10px;
  font-size: 16px;
  border: 1px solid #ccc;
  border-radius: 5px;
  outline: none; 
  transition: border-color 0.3s ease;
}

input:focus {
  border-color: #007bff;
  box-shadow: 0 0 5px rgba(0, 123, 255, 0.5);
}

.message {
  margin-right: 0.5rem;
}

button {
  display: inline-block;
  padding: 10px 20px;
  font-size: 16px;
  font-weight: bold;
  text-align: center;
  text-decoration: none;
  cursor: pointer;
  border: none;
  border-radius: 5px;
  transition: background-color 0.3s ease, color 0.3s ease, box-shadow 0.3s ease;
}

button.default {
  background-color: #fff;
  color: #000;
}

button.default:hover {
  background-color: #000;
  color: #fff;
}

button.default:active {
  background-color: #303030;
}
</style>
