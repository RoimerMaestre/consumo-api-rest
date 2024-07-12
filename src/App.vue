<template>
  <main v-if="user1 && user2">
    <!-- fomularios -->
    <form @submit.prevent="enviarMensaje('user1')">
      <img :src="user1.picture.large" alt="">
      <p>{{ user1.name.first }} {{ user1.name.last }}</p>
      <input type="color" v-model="mensaje1.color">
      <textarea v-model="mensaje1.texto"></textarea>
      <button type="submit">Enviar</button>
    </form>

    <ChatInteractivo :mensajes="mensajes" :user1="user1" :user2="user2"/>

    <form @submit.prevent="enviarMensaje('user2')">
      <img :src="user2.picture.large" alt="">
      <p>{{ user2.name.first }} {{ user2.name.last }}</p>
      <input type="color" v-model="mensaje2.color">
      <textarea v-model="mensaje2.texto"></textarea>
      <button type="submit">Enviar</button>
    </form>
  </main>
</template>

<script>
import axios from 'axios';
import ChatInteractivo from './components/ChatInteractivo.vue';

export default {
  name: 'App',
  components: {
    ChatInteractivo,
  },
  data() {
    return {
      user1: null,
      user2: null,
      mensaje1: { texto: '', color: '#FFA833' },
      mensaje2: { texto: '', color: '#FF6133' },
      mensajes: [],
    };
  },
//ciclo de vida
//se aprendio que hay varios ciclos de vida, o hooks, conocia el mounted, y estudiando vimos los demas, sin embargo aun no comprendo bien su funcionalidad 
  async created() {
    try {
      const response = await axios.get('https://randomuser.me/api?results=2');
      this.user1 = response.data.results[0];
      this.user2 = response.data.results[1];
    } catch (error) {
      console.error(error);
    }
  },
  methods: {
    enviarMensaje(user) {
      const mensaje = user === 'user1' ? this.mensaje1 : this.mensaje2;
      const propietario = user === 'user1' ? this.user1 : this.user2;

      this.mensajes.push({
        texto: mensaje.texto,
        color: mensaje.color,
        propietario: `${propietario.name.first} ${propietario.name.last}`,
        id: user
      });

      // Limpiar el formulario
      mensaje.texto = '';
      
    },
  },
};
</script>

<style>
main {
  display: flex;
  justify-content: center;
  gap: 10px;
  padding: 20px;
}

form {
  width: 200px;
  height: 400px;
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 15px;
  border: 2px solid #ddd;
  border-radius: 10px;
  background-color: #fff;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

img{
  width: 100%;
  object-fit: cover;
}


textarea {
  width: 100%;  
  height: 100px;
  margin-bottom: 10px;
  resize: none; 
}

input {
  width: 100%; 
  height: 30px; 
  margin-bottom: 10px; 
}

button {
  width: 100%;
  margin-top: 10px;
}
</style>
