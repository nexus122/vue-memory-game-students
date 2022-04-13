<!-- ChessBoard Component -->
<script setup>
import Card from "./Card.vue";
import { reactive } from "vue";

// Props que nos pasa el padre
const props = defineProps({
  cards: Array,
  backCardImage: String,
});

// Emits que le pasamos al padre.
const emit = defineEmits(['onCheckedCards'])

let cardsCheesBoard = props.cards.concat(props.cards);
let selectedCards = [];
// reactive -> objetos y arrays
// ref -> primitivas, (string, number)
cardsCheesBoard = reactive(
  cardsCheesBoard.map((card) => {
    return {
      ...card,
      reveal: false,
    };
  })
);

console.log(cardsCheesBoard);

function onCardClicked(card) {
  if (card.reveal || selectedCards.length == 2) {
    return;
  }

  // Mostramos la carta seleccionada
  card.reveal = true;
  // Añadimos la carta seleccionada al array de cartas seleccionadas
  selectedCards.push(card);
  // Si ya hemos seleccionado 2 cartas las comparamos
  if (selectedCards.length == 2) {
    // Guardamos la condición en una variable.
    const isMatch = selectedCards[0].id != selectedCards[1].id;

    // Emitimos un evento al padre diciendo true o false, si lo hemos hecho mal o bien.
    emit('onCheckedCards', isMatch)

    if (isMatch) {
      // Si son distintas les damos la vuelta
      selectedCards[0].reveal = false;
      selectedCards[1].reveal = false;
    }
    
    selectedCards = [];
  }
}
</script>

<template>
  <!-- Iteración 3, crear tantas cards como elementos hay en cards -->
  <article>
    <Card
      @click="onCardClicked(card)"
      v-for="card in cardsCheesBoard"
      :key="card.id"
      :back="backCardImage"
      :front="card.img"
      :reveal="card.reveal"
    />
  </article>
</template>

<style scoped>
article {
  display: grid;
  grid-template-columns: repeat(5, 1fr);
  row-gap: 1rem;
}
</style>