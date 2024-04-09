<script setup>
    defineProps(["inicio", "fin", "maxLength"]);
    const emit = defineEmits(['next', 'prev'])

    const activarSiguiente = () => {
        console.log('me diste a siguiente')
        emit('next')
    }
    const activarAtras = () => {
        console.log('TU ESTAS PENDEJO HIJO')
        emit('prev')
    }
</script>

<template>
<div class="btn-group" role="group" aria-label="Basic example">
  <button 
    type="button" 
    @click="activarAtras" 
    class="btn btn-primary"
    :disabled="inicio <= 0"
   >
        Previeus
    </button>
  <button 
    type="button" 
    @click="activarSiguiente" 
    class="btn btn-primary"
    :disabled="fin >= maxLength"
    >
        Next
   </button>
</div>
</template>