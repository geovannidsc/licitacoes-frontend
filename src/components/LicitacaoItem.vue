<template>
  <li>
    <div class="button-container">
    <button 
      :class="['lida-button', isChecked ? 'lida' : 'nao-lida']"
      @click="toggleLida"
    >
      {{ isChecked ? 'Lida' : 'Não Lida' }}
    </button>
  </div>
    <h3>{{ licitacao.orgaoResponsavel }}</h3>
    <h4>{{ licitacao.setorSolicitante }}</h4>
    <h4>Código da UASG: {{ licitacao.codigoUasg }}</h4>
    <h4>{{ licitacao.pregao }}</h4>
    <p><b>Edital a partir de:</b> {{ licitacao.editalAPartirDe }}</p>
    <p>{{ licitacao.objeto }}</p>
    <p><b>Endereço:</b> {{ licitacao.endereco }}</p>
    <p><b>Telefone:</b> {{ licitacao.telefone }}</p>
    <p>Entrega da Proposta: {{ licitacao.entregaProposta }}</p>
    <button @click="mostrarItens = !mostrarItens" class="ver-itens-btn">
      Ver Itens
    </button>
    <ItensLicitacao v-if="mostrarItens" :itens="licitacao.itensEdital" @fechar="mostrarItens = false" />
  </li>
</template>

<script>
import '../styles/LicitacaoItem.css';
import ItensLicitacao from './ItensLicitacao.vue'; 

export default {
  components: {
    ItensLicitacao
  },
  props: {
    licitacao: {
      type: Object,
      required: true
    }
  },
  data() {
    return {
      mostrarItens: false,
      isChecked: this.licitacao.lida 
    };
  },
  methods: {
  async toggleLida() {
    // Inverte o estado local
    this.isChecked = !this.isChecked;

    try {
      const response = await fetch(`http://localhost:8080/api/licitacoes/alternar-leitura?numeroPregao=${this.licitacao.numeroPregao}&codigoUasg=${this.licitacao.codigoUasg}`, {
        method: 'PUT',
        headers: {
          'Content-Type': 'application/json'
        }
      });

      if (!response.ok) {
        throw new Error('Erro ao marcar como lida');
      }

      this.$emit('update-lida', { ...this.licitacao, lida: this.isChecked });

    } catch (error) {
      console.error('Erro ao atualizar o status da licitação:', error);
      this.isChecked = !this.isChecked;
    }
  }

  },
  watch: {
    licitacao: {
      handler(newVal) {
        this.isChecked = newVal.lida; 
      },
      deep: true
    }
  }
};
</script>

