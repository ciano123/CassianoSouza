<template>
    <div class="question-title">Questão 2</div>
    <div class="question-title">Dropdown:</div>
    <div class="question-text">
        Transforme a estrutura dada em um seletor dropdown (como um <tt>&#60;select/&#62;</tt>)
        a partir das opções dadas em <tt>:opcoesDD</tt>, indicando a opção atualmente selecionada
        no texto do seletor e visualmente na lista de opções. A opção padrão deve ser inicialmente
        a primeira opção dada na lista. Crie também uma função que retorne a opção selecionada no
        formato <tt>[ texto, idx ]</tt> ('texto' sendo a opção em si, e 'idx' seu índice na lista)
        para leitura pelo componente pai.
    </div>

    <div @click.stop.prevent="toggle()" class="dropdown" :class="{'down': estado}"> {{ opcaoSelecionada }} ⬇ </div>
    <div v-show="isOpen" :class="{'opcoes': estado}">
    <div class="drop-op">
         <ul v-for="(opcao, idx) in opcoesDD" :key="idx.id" @click="set(opcao)">
        <!-- OPÇÕES PASSADAS (INDICANDO A ATUAL SELECIONADA) -->
        <tt>{{idx}} - {{ opcao }}</tt>
        
    </ul>
    </div>
    </div>
   
</template>

<script>
    export default {
        name: "DropDown",
        props: {
            opcoesDD: Array,
        },
        data() {
            return {
                opcaoSelecionada: "Dropdown",
                 isOpen: false,
                // The selected value.
            };
        },
        computed: {
            estado() { return true; }
        },
         methods: {
             toggle: function() {
             this.isOpen = !this.isOpen;
             },
         show: function() {
             this.isOpen = true;
          },
            hide: function() {
                this.isOpen = false;
         },
          // Set option as    selected state and close dropdown.
            set: function(input) {
                 this.opcaoSelecionada = input;
                 this.hide();
             },
            clickOut(evt){
                if (!this.$el.contains(evt.target)){
                    this.hide();
                }
            },
                 onChange() {
            console.log(this.opcaoSelecionada);
            }
         },
         mounted: function() {
             document.addEventListener('click', this.clickOut);
           
            }
        // Atualizar dados com opções passadas...
    }
</script>

<style scoped>
 .dropdown {
     display: flex;
     justify-content: space-around;
     cursor: pointer;
     border: 1px solid #2c3e50;
     border-radius: 5px;
     width: fit-content;
     padding: 5px;
 }

 .down { 
     display: flex;
     justify-content: center;
     position: relative;
     width: 13%;
     border-bottom: 3px solid #2c3e50;
  }
.opcoes ul{
    height: auto;
    display: flex;
    justify-content: space-around;
    flex-direction: column;
    position: relative;
}
 .opcoes{
     width: 15%;
     height: auto;
     background-color: #40E0D0;
     margin-right: 10px;
     display: flex;
     position: relative;
     justify-content: space-around;
     flex-direction: row;
     border-radius: 20px;    

   }
   .opcoes tt{
       font-weight: bold;
       text-shadow: 2px 1px 0px rgb(196, 193, 193);
       font-size: 1.1rem;
       display: flex;
       align-items: center;
       justify-content: space-around;
       margin-right: 36px;
       width: 14vw;
       height: 6vh;
       margin-top: 0;
       margin-bottom: 0;
       border-radius: 10px;
       cursor: pointer;
   }
   .opcoes tt:hover{
       background-color: orangered;
       color: aliceblue;
       text-shadow: 2px 1px 0px rgb(7, 7, 7);
       border-bottom: 3px solid #4169E1;
       transition: ease-in .3s;
   }
</style>
