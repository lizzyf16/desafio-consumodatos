<template>
  <div id="app" class="container">
    <header>
      <h1 class="text-center">Sala Virtual</h1>
    </header>
    <div class="row">
      <div class="col-3" v-if="usuarios.length">
        <cardUsuario
      :imagenUsuario="usuarios[0].picture.large"
      :nombre="usuarios[0].name.first"
      alineacion="left"
      @enviarChat="agregarMensaje"/>
      </div>
      <div class="col-6">
        <cardChat :mensajes="mensajes"/>
      </div>
      <div class="col-3" v-if="usuarios.length">
        <cardUsuario
    :imagenUsuario="usuarios[1].picture.large"
    :nombre="usuarios[1].name.first" 
    alineacion="right"
    @enviarChat="agregarMensaje"/>
      </div>
    </div>


    <!-- <section class="galeria">
        <div v-for="(usuario, index) in usuarios" :key="index">
          <img :src="usuario.picture.large" :alt="usuario.name.first">
          <p></p>
          color
        </div>
      </section> -->
  </div>
</template>

<script>
import axios from 'axios';
import cardChat from './components/cardChat.vue';
import cardUsuario from './components/cardUsuario.vue';

export default {
  name: 'App',
  components: {
    cardChat,
    cardUsuario
  },
  async mounted() {
    try {
      let response = await axios.get("https://randomuser.me/api/?results=2");
      let { data } = response;
      this.usuarios = data.results;
    } catch (error) {
      console.log(error);
      if (error.code == "ERR_NETWORK") {
        return alert("En estos momento el servidor está caído, puede intentar más tarde.")
      }
      if (error.response.status == 404) {
        alert("El recurso que está buscando no existe.");
      } else {
        alert("El servidor en estos momentos no puede procesar su solicitud.")
      }
    }
  },
  data() {
    return {
      usuarios: [],
      mensajes: []
    }
  },
  methods:{
    agregarMensaje: function(nuevoMensaje){
      this.mensajes.push(nuevoMensaje)
    }
  }
}
</script>

<style>
#app {
  font-family:'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
