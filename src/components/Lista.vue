<template>
    <div class="question-title">Questão 3</div>
    <div class="question-title">Edição de entradas:</div>
    <div class="question-text">
        Modifique este componente para que exiba as entradas da lista de objetos (com a estrutura abaixo) cujas as propriedades devem ser inputs no componente <tt>div.entrada</tt>, atualizando
        seus valores no componente pai caso editadas. Cada objeto na lista deve pertencer ao seu próprio elemento. Exiba todos corretamente, exiba os indicadores corretos e repasse os dados ao componente pai ao se clicar no botão atualizar.
        <br />
        <pre class="json-example"><i>// Entrada:</i>
<code>{
    id: Number,
    op1: String,
    op2: String
}</code></pre>
    </div>

    Indicadores:
    <ul>
        <li v-if="placeholder">LISTA VAZIA</li>
        <li v-if="placeholder">MAIS DE 5 ELEMENTOS</li>
        <li v-if="placeholder">UMA OU MAIS ENTRADAS NÃO RESPEITA O FORMATO</li>
    </ul>

    <div class="entradas">   

        <form @submit.prevent="addLista(list)" >
            <div  class="entrada">
                 <h2>Digite as Entradas</h2>
            <label for="text" class="desc-id">Id: </label>
            <input type="text" v-model="list.description" placeholder="Digite seu id">
            <br>
            <label for="text" class="desc-add">Opção 1: </label>
             <input type="text" v-model="list.op1" placeholder="Digite a opção 1">
            <br>
            <label for="text" class="desc-add">Opção 2: </label>
             <input type="text" v-model="list.op2" placeholder="Digite a opção 2">
             <button class="btn-list">Enviar</button>
        </div>
        </form>  
         </div>      
     <div class="list-tog" >
            <div class="list-dados" v-for="(op, i) in lista" :key="i.id" @toggle="togglelist" :list="op">
               <pre class="json-example"><i>// Entradas:</i>         
<code>{
    id: {{ op.description }},
    op1: {{ op.op1 }},
    op2: {{ op.op2 }}
}</code></pre>
            </div>
        </div>

    <button type="submit" @click="update()" class="form-button">Atualizar</button>
</template>

<script>
    export default {
        name: "Lista",
        props: {
            dados: {
                type: Array,
                required: true
            }
        },
        data() {
            return {
                lista: [""], // deve representar a lista dada
                list: {
                    checked: false
                }
            };
        },
         methods: {
            update(){
               
            },
            addLista(list){
                list.id = Date.now();
                this.lista.push(list);
                this.list = {checked: false};
            },
            togglelist(list){
                const index = this.lista.findIndex[item => item.id === list.id];
                if(index > -1){
                    const checked = !this.lista[index].checked;
                    this.$set(this.lista, index, { ...this.lista[index], checked });
                }
            }
        },
        watch: {},
        computed: {
            placeholder() { return true; },
        },
       
    }
</script>

<style scoped>
 .form-button {
     font-size: 1.15rem;
     border-radius: 10px;
     border: 1px solid grey;
     background-color: #2c3e50;
     display: block;
     margin: 0 auto;
     padding: 5px;
     color: whitesmoke;
     cursor: pointer;
 }

 .entradas {
     width: 100%;
     display: flex;
     justify-content: center;
     align-items: center;
     margin: 10px;
 }

 .entrada {
     /* ... */
    padding: 10px;
    background-color: #B0C4DE;
    width: 100%;
    min-width: 400px;
    min-height: 225px;
    border-radius: 20px;
    
 }
 .entrada h2{
    font-family: Cambria, Cochin, Georgia, Times, 'Times New Roman', serif;
    font-weight: bold;
    font-size: 20px;
    display: flex;
    justify-content: center;
    margin-bottom: 15px;
    padding-bottom: 10px;
    color: #D2691E;
 }
 .entrada label{
    font-size: 16px;
    font-family: Cambria, Cochin, Georgia, Times, 'Times New Roman', serif;
    font-weight: bold;
    padding-right: 10px;
    padding: 10px;
 }
 .entrada .desc-id{
    padding-left: 53px;
 }
.entrada input{
    padding-top: 10px;
    margin-top: 5px;
    border-radius: 5px;
    border: 2px solid #696969;
    background-color: 	#F0F8FF;
}
.entrada input:hover{
    background-color: #FFF5EE;
    border: 2px solid #D2691E;
}
.entrada button{
    display: flex;
    justify-content: space-around;
    position: relative;
    margin-top: 15px;
    margin-left: auto;
    margin-right: auto;
    width: 150px;
    height: 6vh;
    padding-top: 8px;
    border-radius: 5px;
    color: orangered;
    font-weight: bold;
    cursor: pointer;
    background-color: #9ACD32;
}
.entrada button:hover{
    background-color: orangered;
    color: #9ACD32;
    border-bottom: 3px solid #9ACD32;
}
 .json-example {
     font-style: normal;
     background-color: lightgrey;
     border: 1px solid #2c3e50;
     padding: 5px;
 }

 .json-example > code {
     font-family: "Courier New", monospace !important;
 }
</style>
