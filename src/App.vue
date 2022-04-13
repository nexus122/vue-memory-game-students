<script setup>
// Importamos el JSON. Vue ya lo convierte en un array de objetos y lo poe en la variable pokedex
import pokedex from "./assets/pokedex.json";
import backCardImage from "./assets/back-card.png";
import Card from "./components/Card.vue";
import ChessBoard from "./components/ChessBoard.vue";
import RadialProgress from "vue3-radial-progress";

import { reactive } from "vue";

// Iteración 1. Haced un console.log para ver el resultado. Sugerencia: cread una variable nueva normal y corriente
let pokemon = reactive([]);
function obtenerPokemons() {
  shuffleArray(pokedex);
  pokemon = pokedex.slice(0, 10);
  pokemon = pokemon.map((p) => {
    return {
      id: p.id,
      name: p.name.english,
      image: `/pokemons/${p.id.toString().padStart(3, "0")}.png`,
    };
  });
}
obtenerPokemons();

const state = reactive({
  score: 0,
  totalMatches: 10,
  tryClicks: 0,
});

function checkCards(isMatch) {
  state.tryClicks++;
  if (isMatch) {
    state.score++;
  }
}

function restart(){
  location.reload();
}

function shuffleArray(inputArray) {
  inputArray.sort(() => Math.random() - 0.5);
}
</script>

<template>
  <h1>¡PokeMemory!</h1>
  <br />
  <header>
    <p class="header--info">Intentos: {{ state.tryClicks }}</p>
    <p class="header--info">
      Encontrados: {{ state.score }}/{{ state.totalMatches }}
    </p>
  </header>

  <button @click="restart" v-if="state.score == state.totalMatches" class="btn">Restart</button>

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
@import url("https://fonts.googleapis.com/css2?family=Press+Start+2P&display=swap");

header {
  line-height: 1.5;
  display: flex;
  flex-wrap: wrap;
  justify-content: space-around;
  width: 100%;
  font-family: "Press Start 2P", cursive;
  text-align: center;
}
h1 {
  font-family: "Press Start 2P", cursive;
}

main {
  margin-top: 2em;
}

.btn {
  padding: 1em;
  font-size: 1em;
  border: 0px;
  background-color: var(--vt-c-indigo);
  color: white;
  cursor: pointer;
  border-radius: 1em;
  min-width: 200px;
  font-family: "Press Start 2P", cursive;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}
.header--info {
  font-size: 2em;
}
.heder--score {
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
