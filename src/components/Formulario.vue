<script setup>
import { computed, reactive } from "vue";
import Alerta from "./Alerta.vue";

const alerta = reactive({
  tipo: "",
  mensaje: "",
});

const emits = defineEmits([
  "update:registro",
  "update:cliente",
  "update:email",
  "update:fecha",
  "update:motivo",
  "update:id",
  "agregar-cita",
]);

const props = defineProps({
  id:{
    type:[String , null],
    required:true
  },
  registro: {
    type: String,
    required: true,
  },
  cliente: {
    type: String,
    required: true,
  },
  email: {
    type: String,
    required: true,
  },
  fecha: {
    type: String,
    required: true,
  },
  motivo: {
    type: String,
    required: true,
  },
});

const editando = computed(()=>{
  return props.id
})

const handleSubmit = () => {
  if (Object.values(props).includes("")) {
    alerta.mensaje='Todos los campos son Obligatorios'
    alerta.tipo='error'
    return;
  }
  emits("agregar-cita");
  alerta.tipo = "success";
  alerta.mensaje = "Datos Resgistrados de manera correcta";

  setTimeout(() => {
    alerta.tipo = "";
    alerta.mensaje = "";
  }, 1500);
};
</script>

<template>
  <Alerta
    v-if="alerta.mensaje"
    v-bind:alerta="alerta"
  />
  <form
    v-on:submit.prevent="handleSubmit"
    class="flex flex-col gap-2 bg-white p-6 rounded-md shadow"
  >
    <div class="content__input">
      <label
        class="text-lg font-medium"
        for="cliente"
        >Cliente Registro</label
      >
      <input
        class="py-2 px-5 border rounded-sm"
        type="text"
        placeholder="cesar zubilete"
        id="cliente"
        @input="$emit('update:registro', $event.target.value)"
        :value="registro"
      />
    </div>
    <div class="content__input">
      <label
        class="text-lg font-medium"
        for="cita"
        >Nombre Cita</label
      >
      <input
        class="py-2 px-5 border rounded-sm"
        type="text"
        placeholder="claudia zubilete"
        id="cita"
        @input="$emit('update:cliente', $event.target.value)"
        :value="cliente"
      />
    </div>
    <div class="content__input">
      <label
        class="text-lg font-medium"
        for="email"
        >Email</label
      >
      <input
        class="py-2 px-5 border rounded-sm"
        type="email"
        placeholder="cesarzubilete@correo.com"
        id="email"
        @input="$emit('update:email', $event.target.value)"
        :value="email"
      />
    </div>
    <div class="content__input">
      <label
        class="text-lg font-medium"
        for="fecha"
        >Fecha Registro</label
      >
      <input
        class="py-2 px-5 border rounded-sm"
        type="date"
        id="fecha"
        @input="$emit('update:fecha', $event.target.value)"
        :value="fecha"
      />
    </div>
    <div class="content__input">
      <label
        class="text-lg font-medium"
        for="motivo"
        >Motivo</label
      >
      <textarea
        class="border resize-none px-5 pt-4"
        name="motivo"
        id="motivo"
        cols="30"
        rows="7"
        @input="$emit('update:motivo', $event.target.value)"
        :value="motivo"
      ></textarea>
    </div>
    <div class="flex justify-center pt-2">
      <input
        :class="[editando ? 'bg-slate-700 hover:bg-slte-700/80' : 'bg-blue-700 hover:bg-blue-700/80']"
        class="btn"
        type="submit"
        :value="[editando ? 'Actualizando' : 'Registrar Datos']"
      />
    </div>
  </form>
</template>
