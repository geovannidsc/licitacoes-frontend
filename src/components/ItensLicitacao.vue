<template>
    <div class="itens-list">
      <h3>Itens da Licitação</h3>
      <ul>
        <li v-for="item in itens" :key="item.id">
          <p>
            <b>ID:</b> {{ item.id }}<br>
            <b>{{ item.nome }}</b> <br>
            <b>Descrição:</b><br>
            <span v-html="formatarDescricao(item.descricao)"></span>
          </p>
        </li>
      </ul>
      <button @click="$emit('fechar')" class="fechar-btn">Fechar</button>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      itens: {
        type: Array,
        required: true
      }
    },
    methods: {
      formatarDescricao(descricao) {
        return descricao.replace(/\|/g, '<br>'); // Substitui | por <br>
      }
    }
  };
  </script>
  

  