<template>
  <div class="container">
   
    <div
      v-for="(mensaje, index) in mensajes"
      :key="index"
      :class="['mensaje', { 'mensaje-propio': mensaje.id === 'user2' }]"
      
    >
      <span>{{ mensaje.propietario }}</span>
      <p class="parrafo" :style="{ backgroundColor: mensaje.color}">{{ mensaje.texto }}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: "ChatInteractivo",
  props: {
    mensajes: Array,
    user1: Object,
    user2: Object
  },
};
</script>

<style scoped>

.container {
  width: 400px;
  height: 400px;
  padding: 15px;
  border: 2px solid #97a3af;
  border-radius: 10px;
  font-size: 16px;
  line-height: 1.5;
  overflow-y: auto;
  background-color: rgb(239, 230, 221);
  box-shadow: 0 0 8px rgba(0, 123, 255, 0.3);
}

.mensaje {
  padding: 10px;
  margin-bottom: 10px;
  border-radius: 5px;
  color: #fff;
}

.mensaje-propio {
  text-align: right;
}

span{
  color:#121110cb ;
}
.parrafo{
  padding: 5px;
  border-radius: 10px;
  overflow: hidden;
  word-wrap: break-word; /* Forzar el salto de línea si la palabra es demasiado larga */
  word-break: break-word; /* Forzar el salto de línea si la palabra es demasiado larga */
  white-space: pre-wrap; /* Mantiene los saltos de línea y espacios */
}
  


</style>
