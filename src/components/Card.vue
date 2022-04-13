<!-- Card Component -->
<script setup>

// Definir propiedades del componente
// La función recibe un parámetro que es un objeto con todas las propiedades del componente
// Se pone nombredelapropiedad: tipo de variable

const props = defineProps({
    back: String, // es una ruta a una imagen
    front: String, // es una ruta a una imagen
    reveal: Boolean // me dice que debo revelarme o no
})

</script>

<template>
    <!-- Podemos usar en el template directamente las propiedades, simplemente poniendo su nomre -->
    <div class="card">
        <TransitionGroup name="slide-fade">
            <img v-if="!reveal" class="front" :src="back" alt="pokemon card">
            <img v-if="reveal" class="back" :src="front" alt="pokemon butterfly">
        </TransitionGroup>
    </div>
</template>

<style scoped>
.card{
    width: clamp(69px, 18vw, 175px);
    height: 170px;
}

.card img{
    width: 100%;
}

/*
  Enter and leave animations can use different
  durations and timing functions.
*/
.slide-fade-enter-active {
    transition: all 0.5s;
}

.slide-fade-leave-active {
    transition: all 0.5s;
}

.slide-fade-enter-from{
    opacity: 1;
    transform: rotateY(-180deg);
}

.slide-fade-leave-to {    
    opacity: 0;
    transform: rotateY(180deg);
}
.back, .front{
    position: absolute;    
}
</style>