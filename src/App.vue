<script setup>
import { ref, reactive } from 'vue';
import{uid} from 'uid';
import Header from './components/Header.vue';
import Formulario from './components/Formulario.vue';
import Paciente from './components/Paciente.vue';

const pacientes = ref([]);

const paciente= reactive({
  id: null,
    mascota: '',
    propietario: '',
    email: '',
    alta: '',
    sintomas: ''
});
const crearPaciente = () => {
    console.log('Creando paciente');
    pacientes.value.push({...paciente , id: uid()});

    Object.keys(paciente).forEach(key => {
      paciente[key] = '';
    });
  }


  constactualizarPaciente=() => {
    console.log('Actualizando paciente');
  }

</script>

<template>
  <div class="container mx-auto mt-20">
   

    <Header /> 

    <div class=" mt-12 md:flex">
      <Formulario
        
          v-model:mascota ="paciente.mascota"
          v-model:propietario ="paciente.propietario"
          v-model:email="paciente.email"
          v-model:alta="paciente.alta"
          v-model:sintomas="paciente.sintomas"
          @guardar-paciente="crearPaciente"
      />
      

      <div class=" md:w-1/2 md:h-screen overflow-y-scroll" >

        <h3 class="font-black text-3xl text-center">  Adminisstra sus Pacientes </h3>

        <div v-if="pacientes.length >0">
          <p class=" text-lg mt-5 text-center mb-10"> Informacion de los 
        <span class="text-indigo-600 font-bold"> Pacientes</span> 


    </p>

          <Paciente 
            v-for="(paciente) in pacientes"
            :paciente="paciente"
            @actualizar-paciente="actualizarPaciente"
          />
            

        </div>
        <p  v-else class="mt-10 text-2xl text-center"> No hay pacientes</p>



      </div>
    

    </div>

  </div>
</template>

