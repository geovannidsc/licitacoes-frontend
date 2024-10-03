<template>
  <div id="app">
    <CabecalhoTopo />
    <main>
      <FiltroLicitacoes @filter="applyFilter" />
      <LoadingSpinner v-if="loading" />
      <ErrorMessage v-if="error" :message="error" @close="error = null" />
      <LicitacoesList v-if="!loading && !error" :licitacoes="licitacoes" />
      <Pagination v-if="!loading && totalPages > 1" :current-page="currentPage" :total-pages="totalPages" @page-changed="changePage" />
    </main>
  </div>
</template>

<script>
import CabecalhoTopo from './CabecalhoTopo.vue'; 
import FiltroLicitacoes from './FiltroLicitacoes.vue';
import LicitacoesList from './LicitacoesList.vue';
import LoadingSpinner from './LoadingSpinner.vue';
import ErrorMessage from './ErrorMessage.vue';
import Pagination from './Pagination.vue';
import '../styles/App.css'; 

export default {
  components: {
    CabecalhoTopo,
    FiltroLicitacoes,
    LicitacoesList,
    LoadingSpinner,
    ErrorMessage,
    Pagination
  },
  data() {
    return {
      licitacoes: [],
      loading: false,
      error: null,
      currentPage: 1,
      totalPages: 1,
      filter: ''
    };
  },
  methods: {
    async fetchLicitacoes() {
      this.loading = true;
      try {
        const response = await fetch(`https://licitacoes-production.up.railway.app/api/licitacoes?page=${this.currentPage - 1}&size=20&termo=${this.filter}`);
        if (!response.ok) {
          throw new Error('Erro ao buscar licitações');
        }
        const data = await response.json();
        this.licitacoes = data.content; 
        this.totalPages = data.totalPages; 
      } catch (err) {
        this.error = err.message;
      } finally {
        this.loading = false;
      }
    },
    applyFilter(filter) {
      this.filter = filter;
      this.currentPage = 1;
      this.fetchLicitacoes();
    },
    changePage(page) {
      this.currentPage = page;
      this.fetchLicitacoes();
    }
  },
  mounted() {
    this.fetchLicitacoes();
  }
};
</script>

<style scoped>
#app {
  font-family: 'Arial', sans-serif;
  color: #2c3e50;
}

main {
  padding: 2rem;
  background-color: #f8f9fa;
  border-radius: 8px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}

h2 {
  color: #2980b9;
  text-align: center;
  margin-bottom: 1.5rem;
}

.loading-spinner {
  display: flex;
  justify-content: center;
  margin: 2rem 0;
}

.error-message {
  color: red;
  text-align: center;
  margin-top: 1rem;
}

.pagination {
  display: flex;
  justify-content: center;
  margin-top: 2rem;
}

.licitacoes-list {
  margin-top: 1rem;
}
</style>
