<template>
    <div v-if="message" class="error-message">
      <p>{{ message }}</p>
      <button @click="closeError">Fechar</button>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      message: {
        type: String,
        required: true,
      }
    },
    methods: {
      closeError() {
        this.$emit('close');
      }
    }
  };
  </script>
  
  <style scoped>
  .error-message {
    background-color: #f8d7da;
    color: #721c24;
    border: 1px solid #f5c6cb;
    padding: 1rem;
    margin: 1rem 0;
    border-radius: 5px;
  }
  
  button {
    background-color: #721c24;
    color: white;
    border: none;
    padding: 0.5rem 1rem;
    border-radius: 5px;
    cursor: pointer;
  }
  </style>
  