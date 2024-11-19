<script setup>
import { reactive, computed } from 'vue';
import Alerta from './Alerta.vue';

const alerta =reactive({
   tipo:'',
    mensaje:''
});

const emit =defineEmits (['update:mascota' , 'update:propietario', 'update:email', 'update:alta', 'update:sintomas', 'guardar-paciente']);

const props = defineProps({
    mascota: {
        type: String,
        required: true
    }, 
    propietario: {
        type: String,
        required: true
    },

    email: {
        type: String,
        required: true
    },
    alta: {
        type: String,
        required: true
    },
    sintomas: {
        type: String,
        required: true
    },
    id: {
        type: [String, null],
        required: true
    }
});



const validar = () => {
    console.log('Validando');

    if (Object.values(props).includes('')) {
    
        alerta.mensaje='Todos los campos son obligatorios';
        alerta.tipo='error';

        return;
    }
    emit('guardar-paciente');
    alerta.mensaje='Paciente almacenado correctamente';
    alerta.tipo='exito';

    setTimeout(() => {
        alerta.mensaje='';
        alerta.tipo='';
    }, 3000);
 
}

const editando = computed(() => {
    console.log("editando al paciente con id "+props.id);
    return (props.id );
});



</script>

<template>

<div class="md:w-1/2">
    <h2 class="font-black text-3xl text-center">Seguimiento pacientes </h2>
    <p class=" text-lg mt-5 text-center mb-10"> Añade Pacientes y 
        <span class="text-indigo-600 font-bold"> Administralos</span>


    </p>
    <Alerta v-if="alerta.mensaje"
    :alerta="alerta" />
    
    <form
    class=" bg-white shadow-md rounded-lg py-10 px-5 mb-10"    
    @submit.prevent="validar"
    >
         
        <div class="mb-5">
            <label
             for="mascota"
            class="block text-gray-700 uppercase font-bold "
          
             >
                Nombre Mascota

            </label>

            <input 
            type="text" 
            id ="mascota"
            placeholder="Nombre Mascota"
            class="w-full mt-2 p-2 border-2 placeholder-gray-400 border-gray-400 rounded-lg"
            :value="mascota"
            @input="$emit('update:mascota', $event.target.value)"
            >

        </div>
        <div class="mb-5">
            <label
             for="propietario"
            class="block text-gray-700 uppercase font-bold "
             >
                Nombre Propietario

            </label>

            <input type="text" 
            id ="propietario"
            
            placeholder="Nombre del  Propietario"
            class="w-full mt-2 p-2 border-2 placeholder-gray-400 border-gray-400 rounded-lg"
            :value="propietario"
            @input="$emit('update:propietario', $event.target.value)"
            >

        </div>

        <div class="mb-5">
            <label
             for="email"
            class="block text-gray-700 uppercase font-bold "
             >
                Email del Propietario

            </label>

            <input 
            type="text" 
            id ="email"
            placeholder="Email del  Propietario"
            class="w-full mt-2 p-2 border-2 placeholder-gray-400 border-gray-400 rounded-lg"
           @input="$emit('update:email', $event.target.value)"
           :value="email"
            >

        </div>

        <div class="mb-5">
            <label
             for="alta"
            class="block text-gray-700 uppercase font-bold "
             >
                Alta

            </label>

            <input 
            type="date" 
            id ="date"
           
            class="w-full mt-2 p-2 border-2 placeholder-gray-400 border-gray-400 rounded-lg"
            :value="alta"
           @input="$emit('update:alta', $event.target.value)"
            >

        </div>


        <div class="mb-5">
            <label
             for="sintomas"
            class="block text-gray-700 uppercase font-bold "
             >
                Sintomas

            </label>

            <textarea
        
            id ="sintomas"
             placeholder="Describe los sintomas de tu mascota"
            class="w-full mt-2 p-2 border-2 placeholder-gray-400 border-gray-400 rounded-lg h-40"
            @input="$emit('update:sintomas', $event.target.value)"
            :value="sintomas"
            > </textarea>

        </div>

        <input
        class="bg-indigo-600 w-full p-3  text-white uppercase font-bold hover:bg-indigo-700 rounded-lg cursor-pointer transition-colors"

         type="submit"
         :value="editando ? 'Editar Paciente' : 'Registrar Paciente'"

        >
    </form>


</div>

</template>