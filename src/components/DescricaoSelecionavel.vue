<script lang="ts">
import Tag from './Tag.vue';

export default {
  components: { Tag },
  props: {
    descricao: { type: String, required: true }
  },
  data() {
    return {
      selecionado: false
    }
  },
  methods: {
    aoClicar() {
      this.selecionado = !this.selecionado

      if (this.selecionado) {
        this.$emit('adicionarMissao', this.descricao)
      } else {
        this.$emit('removerMissao', this.descricao);
      }
    }
  },
  emits: ['adicionarMissao', 'removerMissao']
}
</script>

<template>
  <button
    class="descricao"
    @click="aoClicar"
    :aria-pressed="selecionado"
  >
    <Tag :texto="descricao" :ativa="selecionado" />
  </button>
</template>

<style scoped>
.ingrediente {
  cursor: pointer;
}
</style>