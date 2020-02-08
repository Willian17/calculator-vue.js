<template>
  <button class="botao"
  @click="$emit('onClique' , caractere)"
  :class="{ operacao , duplo , triplo}"
  >
 {{caractere}}
  </button>
</template>

<script>
export default {
  props:{
    caractere: {},
    operacao: {type: Boolean},
    duplo: {type :Boolean},
    triplo: {type : Boolean}
  }
}
</script>

<style>
  :root{
    --fundo-botao: #f0f0f0;
    --borda-botao: 1px solid #888;
  }
  .botao{
    font-size: 1.4em;
    background-color: var(--fundo-botao);
    border: none;
    border-right: var(--borda-botao);
    border-bottom: var(--borda-botao);
    outline: none;
  }
  .botao:active{
    background: #CCC
  }
  .duplo{
    grid-column: span 2;
  }
  .triplo{
    grid-column: span 3;
  }
  .operacao{
    background: #fa8231;
    color: white;
  }
  .operacao:active{
    background-color: #fa8231CC
  }
</style>