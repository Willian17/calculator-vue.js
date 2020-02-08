<template>
    <div id="app">
        <h1>Calculadora</h1>
      <Calculadora />
    </div>
</template>

<script>
import Calculadora from './main/Calculadora'
export default {
  components:{Calculadora}
}
</script>

<style>

    @font-face {
        font-family: "Calculator";
        src: url("./fonts/Calculator.ttf");
    }
    *{
        font-family: "Calculator" , monospace
    }
    body{
        margin:  0
    } 
    #app{
        display: flex;
        height: 100vh;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        text-align: center;
        color: white;
        background: linear-gradient(to right, #2b5876, #4e4376); 
    }
</style>

