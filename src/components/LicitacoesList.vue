<template>
    <div>
      <h3>Lista de Licitações</h3>
      <ul>
        <LicitacaoItem v-for="licitacao in licitacoes" :key="licitacao.id" :licitacao="licitacao" />
      </ul>
    </div>
  </template>
  
  <script>
  import LicitacaoItem from './LicitacaoItem.vue';
  import '../styles/LicitacoesList.css';

  export default {
    components: {
      LicitacaoItem
    },
    props: {
      licitacoes: {
        type: Array,
        required: true
      }
    }
  };
  </script>

  