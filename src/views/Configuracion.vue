<template>
  <!-- Contenedor principal de la configuración de usuario -->
  <div class="informe">
    <h1>Configuración de Usuario</h1>
    <!-- Muestra la imagen de perfil si hay una URL válida -->
    <img v-if="urlPerfil" :src="urlPerfil" alt="Imagen de perfil" class="perfil-imagen" >
    <!-- Formulario para editar la configuración de usuario -->
    <form @submit.prevent="guardarDatosUsuario">
      <label for="perfil">Imagen del perfil:</label><br>
      <!-- Input para ingresar la URL de la foto de perfil -->
      <input class="cajas-datos" type="text" id="perfil" v-model="urlPerfil" placeholder="Ingrese la URL de su foto de perfil."><br>
      <label for="nombre">Nombre de Usuario:</label><br>
      <!-- Input para ingresar el nombre de usuario -->
      <input class="cajas-datos" type="text" id="nombre" v-model='nombreUsuario' placeholder="Ingrese su Nombre de Usuario."><br>
      <!-- Botón para guardar los datos -->
      <button class="btn-perfil" type="submit">Guardar</button>
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      nombreUsuario: '', // Almacena el nombre de usuario
      urlPerfil: ''      // Almacena la URL de la foto de perfil
    };
  },
  created() {
    // Obtiene los datos actuales del usuario desde localStorage (si existen)
    this.nombreUsuario = localStorage.getItem('nombreUsuario') || '';
    this.urlPerfil = localStorage.getItem("urlPerfil") || '';
  },
  methods: {
    guardarDatosUsuario() {
      // Guarda el nombre de usuario y la URL de perfil en localStorage
      localStorage.setItem('nombreUsuario', this.nombreUsuario);
      localStorage.setItem('urlPerfil', this.urlPerfil);

      // Emite un evento para notificar a otros componentes que los datos han cambiado
      this.$emit('datos-actualizados', {
        nombreUsuario: this.nombreUsuario,
        urlPerfil: this.urlPerfil 
      });

      // Muestra una alerta al usuario
      alert(`Se ha actualizado su información. Es necesario actualizar la página.`);
    }
  }
}
</script>

<style>
/* Estilos CSS para el componente */
.informe {
  border: 2px solid black;
  margin: auto;
  width: 50%;
  text-align: center;
  border-radius: 12px;
  font-size: 18px;
}

.perfil-imagen {
  width: 150px;
  height: 150px;
  border-radius: 50%;
  border: 1px solid black;
}

.cajas-datos {
  width: 300px;
  height: 40px;
  border: none;
  border-bottom: 2px solid black;
  transition: 0.5s ease;
  margin-bottom: 20px;
  transition: box-shadow 0.3s ease;
}

.cajas-datos:hover {
  transition: 0.1s ease;
  border-radius: 5px;
  box-shadow: inset 0 0 4px black;
}

.cajas-datos::placeholder {
  font-weight: bold;
}

.btn-perfil {
  margin-bottom: 20px;
  width: auto;
  padding: 15px;
  border-radius: 30px;
  font-weight: 600;
  font-size: 14px;
  border: 1px solid #8F9092;
  background-image: linear-gradient(to top, #D8D9DB 0%, #fff 80%, #FDFDFD 100%);
  color: aliceblue;
  cursor: pointer;
  transition: all 0.2s ease;
  font-family: "Source Sans Pro", sans-serif;
  color: #606060;
  text-shadow: 0 1px #fff;
}

.btn-perfil:hover {
  box-shadow: 0 4px 3px 1px #FCFCFC, 0 6px 8px #D6D7D9, 0 -4px 4px #CECFD1, 0 -6px 4px #FEFEFE, inset 0 0 3px 3px #CECFD1;
}

.btn-perfil:active {
  box-shadow: 0 4px 3px 1px #FCFCFC, 0 6px 8px #D6D7D9, 0 -4px 4px #CECFD1, 0 -6px 4px #FEFEFE, inset 0 0 5px 3px #999, inset 0 0 30px #aaa;
}

.btn-perfil:focus {
  box-shadow: 0 4px 3px 1px #FCFCFC, 0 6px 8px #D6D7D9, 0 -4px 4px #CECFD1, 0 -6px 4px #FEFEFE, inset 0 0 5px 3px #999, inset 0 0 30px #aaa;
}

h1 {
  color: black;
  padding: 20px;
}

p {
  color: black;
}

label {
  color: black;
}
</style>
