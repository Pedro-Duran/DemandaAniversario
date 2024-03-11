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
    <div class="missao__bazicash">{{ missao.bazicash }} Bazicash</div>
    <div class="missao__conteudo">
      <h2 class="missao__nome">{{ missao.nome }}</h2>
      <p class="missao__descricao">{{ missao.descricao }}</p>
    </div>
  </article>
</template>


<style scoped>
.missao {
  width: 100%;
  padding: 1rem;
  border-radius: 1rem;
  background: var(--branco, #FFF); /* Mantém o fundo geral do card branco */
  display: flex;
  align-items: center; /* Centraliza os filhos verticalmente */
  gap: 2rem;
}

.missao__bazicash {
  flex: 0 1 auto; /* Não cresce, mas pode encolher */
  font-weight: bold;
  font-size: 1.5rem; /* Aumente o tamanho da fonte conforme necessário */
  color: var(--branco, #FFF); /* Altera a cor do texto para branco para contraste */
  background-color: #754EA9; /* Define a cor de fundo para a cor hexadecimal fornecida */
  padding: 0.5rem 1rem; /* Adiciona um pouco de padding para espaço ao redor do texto */
  border-radius: 0.5rem; /* Adiciona bordas arredondadas para estética */
}

.missao__conteudo {
  display: flex;
  flex-direction: column; /* Organiza título e descrição verticalmente */
  flex: 1; /* Ocupa o espaço restante */
}

.missao__nome {
  margin: 0; /* Remove a margem padrão do h2 */
  color: var(--verde-medio, #3D6D4A);
  font-weight: 700;
  text-align: left;
}

.missao__descricao {
  color: var(--cinza-escuro, #333);
  text-align: left;
}
</style>
