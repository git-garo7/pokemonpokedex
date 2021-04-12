<template>
  <div id="app">
    
    <div class="column is-half is-offset-one-quarter"><!--is -half=ocupar metade da tela-->
        <img src="./assets/pokemon.png"><!-- a imagem dentro da coluna fica mais compactada-->
      <hr>
       <h4 class="is-size-3" >PokedeX</h4><!--bulma diminui po texto ,sendo necessário uma class-->
        <input type="text" placeholder="Buscar pokemon pelo nome" v-model="busca" class="input is-primary">
          <button class="button is-success is-loading" id="loadBtn" >Buscar</button><!-- adicionar@click após a id pra acrescentar botão para click em um mecanismo de busca mais leve,para trocar o botão acessar= https://bulma.io/documentation/elements/button/ -->     
      <div v-for="(poke,index) in resultadoBusca " :key="poke.url"><!--trocar resultadoBusca por "pokemons" para mecanismo de busca mais leve-->
            <Pokemon :name="poke.name" :url="poke.url" :num="index+1"/>
            
        </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import Pokemon from './components/Pokemon';
export default {
  name: 'App',
  data(){
    return{
      pokemons: [],
      //filterdPokemons: [],descomentar pra mecanismo de busca mais leve
      busca:''
    }
  },
  created: function(){
      axios.get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0").then(res => {
      this.pokemons = res.data.results;
     // this.filteredPokemons = res.data.results; descomentar para mecanismo de busca mais leve
      })
  },
  components:{
    Pokemon
  },
 // methods:{
    //buscar: function(){
      //this.filteredPokemons = this.pokemons;
      //if(this.busca == '' ||this.busca == ' ' ){
        //this.filteredPokemons = this.pokemons;        
      //}else{
        //this.filteredPokemons = this.pokemons.filter(pokemon => pokemon.name ==this.busca);
      //}

    //}
  //},descomentar para mecanismo de busca mais leve
  computed:{
    /*comentar o resultado busca caso queira um mecanismo de busca mais leve*/
    resultadoBusca: function(){
      if(this.busca == '' ||this.busca == ' ' ){
        return this.pokemons;
      }else{
        return this.pokemons.filter(pokemon => pokemon.name ==this.busca)
      }
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;

}
#loadBtn{
    margin-top: 2%;
  }
</style>
<!--veja mais sobra as culunas do BULMA em = https://bulma.io/documentation/columns/basics/-->
<!--mecanismo de busca mais leve trata-se de pesquisar escrevendo o nome do pokemon e clicando no botão para pesquisar,diferente do que esta agora-->