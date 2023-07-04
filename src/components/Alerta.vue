<script setup>
  defineProps({
    alerta:{
      tipo:Object,
      required:true
    }
  })

</script>
<template>
  <div 
    :class="[alerta.tipo === 'error' ? 'bg-red-500' : 'bg-blue-500']"
    class="py-3 text-white rounded-md text-center font-medium mb-4">
    {{alerta.mensaje}}
  </div>
</template>