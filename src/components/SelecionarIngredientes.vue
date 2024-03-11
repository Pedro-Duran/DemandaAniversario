<script lang="ts">
import { obterMissoes } from '@/http/index'; 
import { obterCategorias } from '@/http/index';
import type IMissao from '@/interfaces/IMissoes';
import type ICategoria from '@/interfaces/ICategoria';
import CardCategoria from './CardCategoria.vue';
import BotaoPrincipal from './BotaoPrincipal.vue';
import CardMissao from './CardMissao.vue'; 

export default {
  name: 'SelecionarIngredientes',
  data() {
    return {
      categorias: [] as ICategoria[],
      missoes: [] as IMissao[]
    };
  },
  async created() {
    this.categorias = await obterCategorias();
     this.missoes = await obterMissoes();
  
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


  
  
    <ul class="missoes">
  <li v-for="missao in missoes" :key="missao.nome">
    <CardMissao
      :missao="missao"
      @adicionar-missao="$emit('adicionarMissao', $event)"
      @remover-missao="$emit('removerMissao', $event)" />
      <br>
  </li>
</ul>


    <p class="paragrafo dica">
      *Atenção: consideramos que você tem em casa sal, pimenta e água.
    </p>

    <BotaoPrincipal texto="Checar missões!" @click="$emit('buscarReceitas')" />
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
.missoes {
  width: 100%; /* Faz com que a lista ocupe toda a largura disponível */
  list-style: none; /* Remove os marcadores padrão da lista */
  padding: 0; /* Remove o padding padrão da lista */
  margin: 0 auto; /* Centraliza a lista se necessário */
}

.missoes li {
  width: 100%; /* Faz com que cada item da lista ocupe a largura total disponível */
  margin-bottom: 1rem; /* Adiciona espaço entre os itens da lista */
}

/* Mantém os estilos originais do card de missão */
.missao {
  width: 100%; /* Faz com que o card de missão ocupe toda a largura disponível da sua linha */
  /* Mantém os outros estilos existentes */
}
</style>