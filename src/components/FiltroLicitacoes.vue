<template>
  <div class="container-filtro">
    <h2>Filtrar Licitações</h2>
    <input
      type="text"
      v-model="filter"
      @keyup.enter="emitFilter"
      placeholder="Filtrar por palavras chaves"
    />
    <button @click="emitFilter">Pesquisar</button>
  </div>
</template>


<script>
import '../styles/FiltroLicitacoes.css';

export default {
  data() {
    return {
      filter: ''
    };
  },
  methods: {
    emitFilter() {
      this.$emit('filter', this.filter);
    }
  }
};
</script>

