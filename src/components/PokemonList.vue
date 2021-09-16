/* eslint-disable */
<!--<template>
  <div>
    <b-table striped hover :items="pokemonList" @onClick="mostrarVista"></b-table>
  </div>
</template>-->
<template>
  <div>
    <b-row id="pokemonList" cols="5">
      <div id="listContainer" v-for="(pokemon, index) in pokemonList" :key="index">
        <b-card id="cardPokemon" hover  v-b-modal.modal-1 @click="getPokeInfo(index + 1)">
          <img id="pokemonImg" :src="imgUrl + (index + 1 + offset) + '.png'"/>
          <b-card-text>{{index + 1 + offset}}.- {{pokemon.name}}</b-card-text>
        </b-card>
      </div>
    </b-row>

    <div id="loaderSpinner" class="text-center" ref="infinitescrolltrigger">
        <b-spinner variant="primary" label="Text Centered"></b-spinner>
    </div>

    <div>
      <b-modal centered title="Pokemon" v-model="showModal" id="modal-1" hide-footer hide-header>
        <b-container>
          <b-row class="mb-1 text-center">
            <b-col cols="3"><label class="my-4 center name">No. {{pokeId}}</label></b-col>
            <b-col><label class="my-4 center name">{{pokeName}}</label></b-col>
            <b-col><img id="pokemonImgInfo"  :src="pokeImg"/></b-col>
          </b-row>
          <hr>
          <div>
            <b-row class="mb-1 text-center">
              <b-col cols="3"><label class="my-4 pokeDetailCard">Exp. </label></b-col>
              <b-col><label class="my-4 pokeDetailCard">{{pokeExp}}</label></b-col>
              <b-col></b-col>
            </b-row>
            <b-row class="mb-1 text-center">
              <b-col cols="3"><p class="my-4 pokeDetailCard">HT.</p></b-col>
              <b-col><label class="my-4 pokeDetailCard">{{pokeHeight/10}} Mts</label></b-col>
              <b-col></b-col>
            </b-row>
            <b-row class="mb-1 text-center">
              <b-col cols="3"><p class="my-4 pokeDetailCard">WT. </p></b-col>
              <b-col><label class="my-4 pokeDetailCard">{{pokeWeight/10}} Kg</label></b-col>
              <b-col></b-col>
            </b-row>
          </div>
          <hr>
          <div>
            <label id="typesCards" v-for="(types, index) in pokeTypes" :key="index" :class="types.type.name"> {{types.type.name}} </label>
          </div>
        </b-container>
      </b-modal>
    </div>
  </div>
</template>


<script>
  import axios from "axios";

  export default {
    data() {
      return {
        offset : 0,
        showModal : false,
        pokemonList: [],
        pokeId: 0,
        pokeName: "",
        pokeExp: 0,
        pokeHeight: 0,
        pokeWeight: 0,
        pokeTypes: [],
        pokeImg: "",
        imgUrl: "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/"
      }
    },
    created(){
      axios.get("https://pokeapi.co/api/v2/pokemon?limit=50&offset=" + this.offset).then((result) => {
        this.pokemonList = result.data.results;
      });
    },
    mounted(){
      this.scrollTrigger();
    },
    methods: {
      getPokeInfo(index){
        axios.get("https://pokeapi.co/api/v2/pokemon/" + (index + this.offset)).then((result) => {
          this.pokeId = result.data.id;
          this.pokeName = result.data.name;
          this.pokeExp = result.data.base_experience;
          this.pokeHeight = result.data.height;
          this.pokeWeight = result.data.weight;
          this.pokeTypes = result.data.types;
          this.pokeImg = this.imgUrl + result.data.id + ".png";
          
      });
      },
      getImgPokemon(){
        document.getElementById("pokemonImgInfo").src = this.imgUrl + this.pokeId + ".png";
      },
      scrollTrigger() {
        console.log("Entre");
        const observer = new IntersectionObserver((entries) => {
          entries.forEach(entry => {
            if(entry.intersectionRatio > 0) {
              this.addMorePokemons();
            }
          });
        });

        observer.observe(this.$refs.infinitescrolltrigger);
      },
      addMorePokemons(){
        axios.get("https://pokeapi.co/api/v2/pokemon?limit=50&offset=" + this.offset).then((result) => {
        if(this.pokemonList.length != 0){
          while(result.data.results.length > 0 && this.pokemonList.length + this.offset < 890){
            this.pokemonList.push(result.data.results.shift());
          }
        }
        });
      }
    }
  }

  
</script>