<script setup>
import { computed } from 'vue';


const props = defineProps({
    alerta: {
        type: Object,
        required: true
    }
})

 const isError =computed(() => {
    return props.alerta.tipo === 'error'; 

 });
</script>
<template>
    <div 
    :class="isError ? ' border-red-500 text-red-700  bg-red-100' : 'border-green-500 text-green-700 bg-green-100' "
    class="
    border-l-4  p-4
      "
       role="alert">
        <p class="font-bold">{{ alerta.tipo.toUpperCase() }}!:</p>
        <p> {{ alerta.mensaje }}</p>
    </div>
</template>