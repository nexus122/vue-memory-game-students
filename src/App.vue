<script setup>
// Importamos el JSON. Vue ya lo convierte en un array de objetos y lo poe en la variable pokedex
import pokedex from "./assets/pokedex.json";
import backCardImage from "./assets/back-card.png";
import Card from "./components/Card.vue";
import ChessBoard from "./components/ChessBoard.vue";
import RadialProgress from "vue3-radial-progress";

import { reactive } from "vue";

// Iteración 1. Haced un console.log para ver el resultado. Sugerencia: cread una variable nueva normal y corriente

shuffleArray(pokedex);

let pokemon = pokedex.slice(0, 10);

// usar .map adecuadamente sobre la variable 'pokemon'. Reasignar el resultado en 'pokemon' solo con los 3 campos requeridos.

// Primera iteración: me quedo solo con el id y el nombre en inglés
// Segunda iteración: Construyo la ruta a la imagen. Por ejemplo para el primer pokemon seria '/pokemons/001.png' , pero para el 10 sería '/pokemons/010.png'
pokemon = pokemon.map((p) => {
  return {
    id: p.id,
    name: p.name.english,
    image: `/pokemons/${p.id.toString().padStart(3, "0")}.png`,
  };
});

const state = reactive({
  score: 0,
  totalMatches: 10,
  tryClicks: 0
});

function checkCards(isMatch) {
  state.tryClicks++;
  if (isMatch) {
    state.score++;    
  }
}

function shuffleArray(inputArray) {
  inputArray.sort(() => Math.random() - 0.5);
}
</script>

<template>
  <h1>¡PokeMemory!</h1>
  <br>
  <header>    
    <p class="header--info">Intentos: {{state.tryClicks}}</p>
    <p class="header--info">Encontrados: {{state.score}}/{{state.totalMatches}}</p>
  </header>

  <main>
    <ChessBoard
      @onCheckedCards="checkCards"
      :cards="pokemon"
      :backCardImage="backCardImage"
    ></ChessBoard>
  </main>
</template>

<style>
@import "./assets/base.css";
@import url('https://fonts.googleapis.com/css2?family=Press+Start+2P&display=swap');

header {
  line-height: 1.5;
  display: flex;
  flex-wrap: wrap;
  justify-content: space-around;
  width: 100%;
  font-family: 'Press Start 2P', cursive;
  text-align: center;
}
h1{
  font-family: 'Press Start 2P', cursive;
}
main{
  margin-top: 2em;
}
.logo {
  display: block;
  margin: 0 auto 2rem;
}
.header--info{
  font-size: 2em;
}
.heder--score{
  font-size: 1em;
}

a,
.green {
  text-decoration: none;
  color: hsla(160, 100%, 37%, 1);
  transition: 0.4s;
}

div#app {
  display: flex;
  flex-wrap: wrap;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  width: 100%;
}

@media (hover: hover) {
  a:hover {
    background-color: hsla(160, 100%, 37%, 0.2);
  }
}

@media (min-width: 1024px) {
  body {
    display: flex;
  }

  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }

  .logo {
    margin: 0 2rem 0 0;
  }
}
</style>
