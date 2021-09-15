/* eslint-disable */
<template>
  <div>
    <b-table striped hover :items="pokemonList" @onClick="mostrarVista"></b-table>
  </div>
</template>

<script>
  import axios from "axios";

  export default {
    data() {
      return {
        pokemonList: []
        /*items: [
          { age: 40, first_name: 'Dickerson', last_name: 'Macdonald' },
          { age: 21, first_name: 'Larsen', last_name: 'Shaw' },
          { age: 89, first_name: 'Geneva', last_name: 'Wilson' },
          { age: 38, first_name: 'Jami', last_name: 'Carney' }
        ]*/
      }
    },
    created(){
      axios.get("https://pokeapi.co/api/v2/pokemon?limit=151").then((result) => {
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