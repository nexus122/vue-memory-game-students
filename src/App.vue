<script setup>
// Importamos el JSON. Vue ya lo convierte en un array de objetos y lo poe en la variable pokedex
import pokedex from "./assets/pokedex.json";

// Componentes
import Card from "./components/Card.vue";
import ChessBoard from "./components/ChessBoard.vue";

// Cargamos imagenes
import backCardImage from "./assets/back-card.png";
import { reactive } from "@vue/reactivity";

// Iteración 1. Haced un console.log para ver el resultado. Sugerencia: cread una variable nueva normal y corriente.
let pokemon = pokedex.slice(0, 10);
// Obtener con el map sobre la variable pokemon, quedarnos con el nombe, la imagen y el identificador unico
pokemon = pokemon.map((p) => {
  return {
    id: p.id,
    name: p.name.french,
    img: "/pokemons/" + p.id.toString().padStart(3, "0") + ".png",
  };
});

// Estado de nuestra aplicación.
const state = reactive({
  score: 0,
});

// Funcion que nos comprueba si hemos hecho algo mal o bien
function checkCards(isMatch) {
  if (!isMatch) {
    state.score++;
  }
}
</script>

<template>
  <header>
    <h1>¡PokeMemory</h1>
    <p>Score: {{ state.score }}</p>
  </header>

  <main>
    <ChessBoard
      @onCheckedCards="checkCards"
      :cards="pokemon"
      :backCardImage="backCardImage"
    />
  </main>
</template>

<style>
@import "./assets/base.css";

header {
  display: flex;
  justify-content: space-between;
  line-height: 1.5;
  padding: 1em;
}

header p {
  vertical-align: middle;
  font-size: 2em;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

a,
.green {
  text-decoration: none;
  color: hsla(160, 100%, 37%, 1);
  transition: 0.4s;
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
