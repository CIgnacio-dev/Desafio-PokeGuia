<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/pokelogo.png">
    <h1>Desafío PokeGuía</h1>
    <label placeholder="Ingresa el Pokémon a buscar">Pokémon:</label>
    <input type="text" v-model='pokemon.name'>
    <button @click='search'>Buscar Pokémon</button>
    <div>
     <img :src="pokeImg">
    </div>
 
    <h2>Movimientos que puede aprender</h2>
    <ul>
      <li v-for=" move in pokeMoves" :key="move">{{move.move.name}}</li>
    </ul>
    <h2 class="ability">Habilidades posibles</h2>
    <ol>
      <li v-for="abilitie in  pokeAbilities" :key="abilitie">{{abilitie.ability.name}}</li>
    </ol>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        pokemon: {
          name: 'pikachu',
          moves: [],
          abilities: [],
        }
      }
    },
    methods: {
      search() {
        let name = this.pokemon.name.toLowerCase()
        fetch(`http://pokeapi.co/api/v2/pokemon/${name}`)
          .then(response => response.json())
          .then(response => this.pokemon = response)
      }
    },
    created() {
      this.search()
    },
    computed: { 
        pokeImg(){
            return this.pokemon.sprites.front_default;
        },
        pokeMoves(){
          return this.pokemon.moves;
        },
        pokeAbilities(){
          return this.pokemon.abilities;
        }

       
      }
     }
  
</script>


<style>
  #app {
    text-align: center; 
    background: rgb(255, 255, 255);
    font-family: 'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;
  }

  img {
    padding-top: 20px;
    margin: 0, auto;
    width: 30vh;
  }

  label {
    margin-right: 10px;
  }
  input {
    border: black, solid;
    width: 30%;
    padding: 10px;
    border: none;
    margin-right: 10px;
  }
  
  
  h2{
    color:aqua;
  }


</style>