<script lang="ts">
import type IMissao from '@/interfaces/IMissoes';
import type { PropType } from 'vue';
import Tag from './Tag.vue';
import DescricaoSelecionavel from './DescricaoSelecionavel.vue';


export default {
  props: {
    missao: { type: Object as PropType<IMissao>, required: true }
  },
  components: { Tag, DescricaoSelecionavel },
  emits: ['adicionarMissao', 'removerMissao']
}
</script>

<template>
  <article class="missao">
    <header class="missao__cabecalho">
      <h2 class="paragrafo-lg missao__nome">{{ missao.nome }}</h2>
    </header>

    <!-- Aqui apenas mostramos a descrição sem iterar, uma vez que é uma string -->
    <p class="missao__descricao">
      {{ missao.descricao }}
    </p>
  </article>
</template>

<style scoped>
.missao {
  width: 19.5rem;
  padding: 1rem;
  border-radius: 1rem;
  background: var(--branco, #FFF);
  box-shadow: 4px 4px 10px 0 rgba(68, 68, 68, 0.05);
  height: auto; /* Alterado para auto para acomodar o conteúdo */

  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 2rem;
}

.missao__cabecalho {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 0.5rem;
}

.missao__nome {
  text-align: center;
  color: var(--verde-medio, #3D6D4A);
  font-weight: 700;
}

.missao__descricao {
  text-align: center;
  color: var(--cinza-escuro, #333);
  /* Adicione mais estilos aqui se necessário */
}
</style>
