/* eslint-disable */
<!--<template>
  <div>
    <b-table striped hover :items="pokemonList" @onClick="mostrarVista"></b-table>
  </div>
</template>-->
<template>
  <div>
    <b-row id="pokemonList" cols="5" width="100%">
      <div id="listContainer" v-for="(pokemon, index) in pokemonList" :key="index">
        <b-card class="card" hover  @onClick="mostrarVista">
          <img id="pokemonImg" :src="imgUrl + (index + 1) + '.png'"/>
          <h1>{{pokemon.name}} {{index + 1}}</h1>
        </b-card>
      </div>
    </b-row>
  </div>
</template>


<script>
  import axios from "axios";

  export default {
    data() {
      return {
        pokemonList: [],
        imgUrl: "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/"
        /*items: [
          { age: 40, first_name: 'Dickerson', last_name: 'Macdonald' },
          { age: 21, first_name: 'Larsen', last_name: 'Shaw' },
          { age: 89, first_name: 'Geneva', last_name: 'Wilson' },
          { age: 38, first_name: 'Jami', last_name: 'Carney' }
        ]*/
      }
    },
    created(){
      axios.get("https://pokeapi.co/api/v2/pokemon?limit=898").then((result) => {
        console.log(result.data.results);
        this.pokemonList = result.data.results;
      });
    },
    methods: {
      mostrarVista: function (item, index, event) {
        /*// this dentro de los métodos apunta a la instancia de Vue
        alert('Hola ' + this.name + '!')
        // evento es el evento DOM nativo
        if (event) {
          alert(event.target.tagName)
        }*/
        console.log(item);
      }
    }
  }

  
</script>