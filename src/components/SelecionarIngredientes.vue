<script lang="ts">
import { obterMissoes } from '@/http/index'; // Importando a função correta
import { obterCategorias } from '@/http/index';
import type IMissoao from '@/interfaces/IMissoes';
import type ICategoria from '@/interfaces/ICategoria';
import CardCategoria from './CardCategoria.vue';
import BotaoPrincipal from './BotaoPrincipal.vue';
import CardMissao from './CardMissao.vue'; // Importe CardMissao

export default {
  name: 'SelecionarIngredientes',
  data() {
    return {
      categorias: [] as ICategoria[],
      missoes: [] as IMissoes[]
    };
  },
  async created() {
    this.categorias = await obterCategorias();
    const missoes = await obterMissoes();
    console.log(missoes)
  },
  components: { CardCategoria, CardMissao, BotaoPrincipal },
  emits: ['adicionarIngrediente', 'removerIngrediente', 'buscarReceitas', 'removerMissao', 'adicionarMissao']
}
</script>

<template>
  <section class="selecionar-ingredientes">
    <h1 class="cabecalho titulo-ingredientes">Missões 🚀</h1>

    <p class="paragrafo-lg instrucoes">
    Cada uma das nossas missões pode te recompensar com bazicash, para você trocar por produtos incríveis!
    </p>

    <ul class="categorias">
      <li v-for="categoria in categorias" :key="categoria.nome">
        <CardCategoria
          :categoria="categoria"
          @adicionar-ingrediente="$emit('adicionarIngrediente', $event)"
          @remover-ingrediente="$emit('removerIngrediente', $event)"
        />
      </li>
    </ul>

    <h2 class="cabecalho">Teste de Missões</h2>
    <ul class="missoes">
      <li v-for="missao in missoes" :key="missao.nome">
        <CardMissao
        :missao="missao"
         @adicionar-missao="$emit('adicionarMissao', $event)"
         @remover-missao="$emit('removerMissao', $event)" />
      </li>
    </ul>

    <p class="paragrafo dica">
      *Atenção: consideramos que você tem em casa sal, pimenta e água.
    </p>

    <BotaoPrincipal texto="Buscar receitas!" @click="$emit('buscarReceitas')" />
  </section>
</template>

<style scoped>
.selecionar-ingredientes {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.titulo-ingredientes, .titulo-missoes {
  color: var(--verde-medio, #3D6D4A);
  display: block;
  margin-bottom: 1.5rem;
}

.instrucoes {
  margin-bottom: 2rem;
}

.categorias, .missoes {
  margin-bottom: 1rem;
  display: flex;
  justify-content: center;
  gap: 1.5rem;
  flex-wrap: wrap;
}

.dica {
  align-self: flex-start;
  margin-bottom: 3.5rem;
}

@media only screen and (max-width: 767px) {
  .dica {
    margin-bottom: 2.5rem;
  }
}

/* Estilos para os cards de missão, adaptados dos estilos de categoria */
.missao {
  width: 19.5rem; /* ou outro valor conforme o design das categorias */
  padding: 1rem;
  border-radius: 1rem;
  background: var(--branco, #FFF);
  box-shadow: 4px 4px 10px 0px rgba(68, 68, 68, 0.05);
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 2rem;
}

.missao__cabecalho {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 0.5rem; /* Corrigido para incluir 'rem' no final e terminar a declaração */
}
</style>