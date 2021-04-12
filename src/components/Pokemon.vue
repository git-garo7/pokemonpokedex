<template>
<div id="pokimao">

   
<!--  <small>{{url}}</small> remover os links-->

     <div class="card">
    <div class="card-image">
        <figure class=""><!--image is-4by3= colocado na classa a imagem ocupa espaço maior mas diminui qualidade-->
        <img :src="currentImg" alt="Placeholder image"><!--pokemon.front é a url onde está armazenada a imagem frontal,troquei por currentImg por uma dinâmica melhor-->
        </figure>
    </div>
    <div class="card-content">
        <div class="media">        
        <div class="media-content">
            <p class="title is-4">{{num}} - {{name | upper}}</p>
            <p class="subtitle is-6">{{pokemon.type}}</p>
        </div>
        </div>

        <div class="content"><!--pode remover o conteúdo mas não a div content,pra não desfigurar o card-->
            <button class="button is-success is-outlined is-medium is-fullwidth" @click="mudarSprite">Mudar Sprite</button><!--encontra em https://bulma.io/documentation/elements/button/ -->
        </div>
    </div>
 </div><!--peguei em = https://bulma.io/documentation/components/card/ -->
    
</div>
  
</template>

<script>
import axios from 'axios';

export default {
    created: function(){
        axios.get(this.url).then(res =>{
            this.pokemon.type = res.data.types[0].type.name;
            this.pokemon.front = res.data.sprites.front_default;
            this.pokemon.back = res.data.sprites.back_default;
            this.currentImg = this.pokemon.front;
        })
    },//created chamado pra cada pokemon da pg
    data(){
        return{
            isFront:true,//controla se o pokemon está de frente ou não
            currentImg: '',
            pokemon:{
                type:'',
                front:'',
                back:''
            }//pro dado ser reativo tem q sr definido em data
        }
    },
    props: {
        num: Number,
        name: String,
        url: String
    },
    filters: {
        upper: function(value){  
            var newName = value[0].toUpperCase()+value.slice(1);//pega toda string se repetir primeira letra
            return newName;
        }
    },
    methods: {
        mudarSprite: function(){
            if(this.isFront){
                this.isFront = false;
                this.currentImg = this.pokemon.back;
            }else{
                this.isFront = true;
                this.currentImg = this.pokemon.front;
            }
        }
    }
}
</script>

<style>
#pokimao{
    margin-top: 2%;
}
</style>