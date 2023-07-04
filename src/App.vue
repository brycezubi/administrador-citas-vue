<script setup>
import { onMounted, reactive, ref, watch } from "vue";
import Titulo from "./components/Titulo.vue";
import Formulario from "./components/Formulario.vue";
import Cita from "./components/Cita.vue";
import { uid } from 'uid';


const citas = ref([]);

const cita = reactive({
  id:null,
  registro: "",
  cliente: "",
  email: "",
  fecha: "",
  motivo: "",
});

watch( citas, ()=>{
  guardarLocalStorage()
},{
  deep:true
})

const guardarLocalStorage =()=>{
  localStorage.setItem('citas', JSON.stringify(citas.value))
}

onMounted(() => {
  const citaStorage = localStorage.getItem('citas')
  citas.value = JSON.parse(citaStorage)
})

const agregarCita = () => {

  if(cita.id){
    const {id} =cita
    const indice = citas.value.findIndex(cita=>cita.id === id);
    citas.value[indice] = {...cita}
  }else{
    citas.value.push({
      ...cita,
      id:uid()
    })
  }

  limpiarCampos();
};

const limpiarCampos = () => {
  return Object.assign(cita, {
    id:null,
    registro: "",
    cliente: "",
    email: "",
    fecha: "",
    motivo: "",
  });
};


const removeCita =(id)=>{
  const citasFiltradas = citas.value.filter( cita=>cita.id !== id)
  citas.value =  citasFiltradas
}

const editarCita = (id)=>{
  const indiceCita = citas.value.findIndex( cita=> cita.id === id)
  const citaEditar = citas.value[indiceCita];
  Object.assign(cita,citaEditar)
}

</script>

<template>
  <Titulo />
  <main class="contenedor grid gap-8 lg:grid-cols-2 lg:gap-16">
    <section>
      <div class="my-5">
        <h2 class="text-center text-2xl text-slate-700 font-medium">
          Registro de Datos
        </h2>
        <h3 class="text-slate-600 pt-2">
          Ingrese los datos en el
          <span class="text-blue-500 font-medium">siguiente formulario</span>
        </h3>
      </div>

      <Formulario
        v-model:registro="cita.registro"
        v-model:cliente="cita.cliente"
        v-model:email="cita.email"
        v-model:fecha="cita.fecha"
        v-model:motivo="cita.motivo"
        v-model:id="cita.id"
        @agregar-cita="agregarCita"
      />
    </section>

    <section>
      <div class="my-5">
        <h2 class="text-center text-2xl text-slate-700 font-medium">
          Citas Registradas
        </h2>
        <h3 class="text-slate-600 pt-2">
          Administra las
          <span class="text-blue-500 font-medium">siguientes citas</span>
        </h3>
      </div>

      <h3
        v-if="citas.length === 0"
        class="text-center text-red-600 font-semibold"
      >
        No Se encuentran citas registradas
      </h3>

      <section v-else class="flex flex-col gap-3 overflow-y-scroll  h-[69vh] pb-4">
        <Cita 
          v-for="cita in citas"
          v-bind:cita="cita"
          @remove-cita="removeCita"
          @editar-cita="editarCita"
        />
      </section>
    </section>
  </main>
</template>
