<script setup>

defineEmits(['remove-cita','editar-cita'])

defineProps({
  cita: {
    type: Object,
    required: true,
  },
});
</script>

<template>
  <article class="bg-white p-6 rounded-md shadow">
    <div class="grid gap-1 lg:grid-cols-2">
      <p class="font-bold text-slate-700">
        Id Cita: <span class="font-normal">{{ cita.id }}</span>
      </p>
      <p class="font-bold text-slate-700">
        Registra Cita: <span class="font-normal">{{ cita.registro }}</span>
      </p>
      <p class="font-bold text-slate-700">
        Cliente: <span class="font-normal">{{ cita.cliente }}</span>
      </p>
      <p class="font-bold text-slate-700">
        Email: <span class="font-normal">{{ cita.email }}</span>
      </p>
      <p class="font-bold text-slate-700">
        Fecha: <span class="font-normal">{{ cita.fecha }}</span>
      </p>
      <p class="font-bold text-slate-700">
        Motivo: <span class="font-normal">{{ cita.motivo }}</span>
      </p>
    </div>
    <div class="flex items-center justify-evenly pt-4">
      <button 
        v-on:click="$emit('editar-cita',cita.id)"
        class="btn bg-blue-500 flex items-center justify-center gap-2">
        Editar
        <svg
          xmlns="http://www.w3.org/2000/svg"
          fill="none"
          viewBox="0 0 24 24"
          strokeWidth="{1.5}"
          stroke="currentColor"
          class="w-5 h-5"
        >
          <path
            strokeLinecap="round"
            strokeLinejoin="round"
            d="M14.74 9l-.346 9m-4.788 0L9.26 9m9.968-3.21c.342.052.682.107 1.022.166m-1.022-.165L18.16 19.673a2.25 2.25 0 01-2.244 2.077H8.084a2.25 2.25 0 01-2.244-2.077L4.772 5.79m14.456 0a48.108 48.108 0 00-3.478-.397m-12 .562c.34-.059.68-.114 1.022-.165m0 0a48.11 48.11 0 013.478-.397m7.5 0v-.916c0-1.18-.91-2.164-2.09-2.201a51.964 51.964 0 00-3.32 0c-1.18.037-2.09 1.022-2.09 2.201v.916m7.5 0a48.667 48.667 0 00-7.5 0"
          />
        </svg>
      </button>
      <button 
        v-on:click="$emit('remove-cita', cita.id)"
        class="btn bg-red-500 flex items-center justify-center gap-2">
        Eliminar
        <svg
          xmlns="http://www.w3.org/2000/svg"
          fill="none"
          viewBox="0 0 24 24"
          strokeWidth="{1.5}"
          stroke="currentColor"
          class="w-5 h-5"
        >
          <path
            strokeLinecap="round"
            strokeLinejoin="round"
            d="M14.74 9l-.346 9m-4.788 0L9.26 9m9.968-3.21c.342.052.682.107 1.022.166m-1.022-.165L18.16 19.673a2.25 2.25 0 01-2.244 2.077H8.084a2.25 2.25 0 01-2.244-2.077L4.772 5.79m14.456 0a48.108 48.108 0 00-3.478-.397m-12 .562c.34-.059.68-.114 1.022-.165m0 0a48.11 48.11 0 013.478-.397m7.5 0v-.916c0-1.18-.91-2.164-2.09-2.201a51.964 51.964 0 00-3.32 0c-1.18.037-2.09 1.022-2.09 2.201v.916m7.5 0a48.667 48.667 0 00-7.5 0"
          />
        </svg>
      </button>
    </div>
  </article>
</template>
