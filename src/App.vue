<template>
  <div>
      <img src="./assets/logo.png" class="logo-pika">
      <h2>PokeGuía</h2>
      Nombre:<input v-model="nombrePoke" @keyup.enter="searchPokemon" type="text" placeholder="Ingresa tu Pokemon">
      <button @click="searchPokemon">Buscar</button>
      <img v-if="namePokemon.sprites" :src="namePokemon.sprites.front_default">
      
      <h3>Movimientos</h3>
      <ul>
          <li v-for="move in moves" :key="move.name">
              {{move.move.name}}
          </li>
      </ul> 
      <h3>Habilidades</h3>
      <ul>
          <li v-for="ability in abilities" :key="ability.name">
              {{ability.ability.name}}
          </li>
      </ul>
  </div>
</template>

<script>
export default {
    data() {
        return {
            namePokemon: {},
            nombrePoke: ""
        }
    },
    created() {
      fetch(`https://pokeapi.co/api/v2/pokemon/pikachu`)
      .then(response => response.json())
      .then(data => this.namePokemon = data)
    },
    methods: {
        searchPokemon () {
            fetch(`https://pokeapi.co/api/v2/pokemon/${this.toPoke}`) 
            .then(data => data.json())
            .then(response => this.namePokemon = response)
        }
    },
    computed:{
        moves() {
            return this.namePokemon.moves
        },
        abilities (){
            return this.namePokemon.abilities
        },
        toPoke() {
            return this.nombrePoke.toLowerCase()
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
}
.logo-pika {
    width: 40vh;
}
li {
    list-style-type: none
}
img { 
    width:120px;
    display: block; 
    margin: auto; 
}

</style>
