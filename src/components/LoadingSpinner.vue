<template>
  <div class="loading">
    <div class="spinner"></div>
    <p>Carregando...</p>
  </div>
</template>

<script>
export default {
  name: 'LoadingSpinner', // Novo nome do componente
};
</script>

<style scoped>
.loading {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 100vh; /* Ocupa toda a altura da tela */
  font-size: 1.5rem;
  color: #007bff; /* Altere a cor conforme necessário */
}

.spinner {
  border: 8px solid #f3f3f3; /* Cor do fundo do spinner */
  border-top: 8px solid #3498db; /* Cor da parte superior do spinner */
  border-radius: 50%;
  width: 40px; /* Tamanho do spinner */
  height: 40px; /* Tamanho do spinner */
  animation: spin 1s linear infinite; /* Animação do spinner */
}

@keyframes spin {
  0% { transform: rotate(0deg); }
  100% { transform: rotate(360deg); }
}
</style>
