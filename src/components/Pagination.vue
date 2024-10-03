<template>
  <div class="pagination">
    <button @click="previousPage" :disabled="currentPage === 1">Anterior</button>
    <span>Página {{ currentPage }} de {{ totalPages }}</span>
    <button @click="nextPage" :disabled="currentPage === totalPages">Próxima</button>
  </div>
</template>

<script>
export default {
  name: 'PaginationControl', // Novo nome do componente
  props: {
    currentPage: {
      type: Number,
      required: true,
    },
    totalPages: {
      type: Number,
      required: true,
    },
  },
  methods: {
    previousPage() {
      if (this.currentPage > 1) {
        this.$emit('page-changed', this.currentPage - 1);
      }
    },
    nextPage() {
      if (this.currentPage < this.totalPages) {
        this.$emit('page-changed', this.currentPage + 1);
      }
    },
  },
};
</script>

<style scoped>
.pagination {
  display: flex;
  align-items: center;
  justify-content: center;
  margin: 1rem 0;
}

button {
  margin: 0 1rem;
  padding: 0.5rem 1rem;
  cursor: pointer;
}
</style>
