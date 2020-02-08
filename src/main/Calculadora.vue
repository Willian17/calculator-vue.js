<template>
  <div class="calculadora">
      <Display :valor="displayValor"/>
      <Button  caractere="AC" triplo @onClique="limparMemoria"/>
      <Button  caractere="/" operacao @onClique="mudarOperacao"/>
      <Button  caractere="7" @onClique="adicionarDigito"/>
      <Button  caractere="8" @onClique="adicionarDigito"/>
      <Button  caractere="9" @onClique="adicionarDigito"/>
      <Button  caractere="*" operacao @onClique="mudarOperacao"/>
      <Button  caractere="4" @onClique="adicionarDigito"/>
      <Button  caractere="5" @onClique="adicionarDigito"/>
      <Button  caractere="6" @onClique="adicionarDigito"/>
      <Button  caractere="-" operacao @onClique="mudarOperacao"/>
      <Button  caractere="1" @onClique="adicionarDigito"/>
      <Button  caractere="2" @onClique="adicionarDigito"/>
      <Button  caractere="3" @onClique="adicionarDigito"/>
      <Button  caractere="+" operacao @onClique="mudarOperacao"/>
      <Button  caractere="0" duplo @onClique="adicionarDigito"/>
      <Button  caractere="." @onClique="adicionarDigito"/>
      <Button  caractere="=" operacao @onClique="mudarOperacao"/>
  </div>
</template>

<script>
import Button from "../components/Button"
import Display from "../components/Display"
export default {
    data: function(){
        return{
            displayValor: '0',
            limparDisplay : false,
            valores : [0,0],
            operacao : null,
            atual: 0,
        }
    },
    components:{Button , Display},
    methods:{
        limparMemoria(){
           Object.assign(this.$data , this.$options.data())
        },
        mudarOperacao(operacao){
           if (this.atual === 0){
               this.atual = 1
               this.limparDisplay = true
               this.operacao = operacao
           } else{
               const igual = operacao === "="
               const operacaoAtual = this.operacao

               try{
                   this.valores[0] = eval(
                       `${this.valores[0]} ${operacaoAtual} ${this.valores[1]}`
                   )
               } catch(e){
                   this.$$emit("onError",  e)
               }

               this.valores[1] = 0

               this.displayValor = this.valores[0]
                this.operacao = igual ? null : operacao
                this.atual = igual ? 0 : 1
                this.limparDisplay = !igual
           }
        },
        adicionarDigito(digito){
            if(digito === '.' && this.displayValor.includes('.')){
                return
            }
            const limparMemoria = this.displayValor === "0" || this.limparDisplay
            const valorAtual = limparMemoria ? '' : this.displayValor
            const novoValor = valorAtual + digito

            this.displayValor = novoValor
            this.limparDisplay = false
            this.valores[this.atual] = novoValor
        }
    }
}
</script>

<style>
 .calculadora{
     display: grid;
     height: 320px;
     width: 235px;
     border-radius: 5px;
     overflow: hidden;

     grid-template-columns: repeat(4 , 25%);
     grid-template-rows: 1fr 48px 48px 48px 48px 48px
 }
</style>