    <!-- Card Component -->
<script setup>
// Asi se definen los props del componente, la función recibe un parametro con un objeto.
// Se pone el nombre de la propiedad y el tipo de la variable.

const props = defineProps({
    back: String,
    front: String,
    reveal: Boolean
})

</script>

<template>
    <div class="card">
        <span v-if="!reveal" class="back"><img :src="back" alt=""></span>
        <span v-else class="front"><img :src="front" alt=""></span>
    </div>
</template>

<style scope>


</style>