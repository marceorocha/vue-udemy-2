<script setup>

defineProps(['inicio', 'fin']);

const emit = defineEmits(['next', 'prev'])

const activarSiguiente = () => {
    console.log('le diste a siguiente');
    emit ('next')
}

</script>

<template>
    <div class="btn-group" role="group" aria-label="Basic example">
        <button 
        @click="emit('prev')" 
        type="button" 
        class="btn btn-outline-primary" 
        :disabled="inicio===0"
        >
        Previous {{ inicio }}
    </button>
        <button 
        @click="activarSiguiente" 
        type="button" 
        class="btn btn-outline-primary"
        :disabled="fin===100"

        >
        Next {{ fin  }}
    </button>

    </div>
</template>