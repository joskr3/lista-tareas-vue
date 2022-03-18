<script >
export default {
  el: '#app',
  data() {
    return {
      estaEditando: false,
      tarea: "",
      tareas: [],
      tareaSeleccionada: null
    }
  },
  methods: {
    guardarTarea() {
      if (this.tarea.trim() === "") {
        return;
      }
      this.tareas.push( this.tarea );
      this.tarea = "";
    },
    eliminarTarea( index ) {
      this.tareas.splice( index, 1 );
    },
    actualizarTarea() {
      this.tareas.splice( this.selectedIndex, 1, this.tarea );
      this.estaEditando = false;
      this.tarea = "";
    },
    editarTarea( index, tarea ) {
      this.estaEditando = true;
      this.tarea = tarea;
      this.selectedIndex = index;
    }
  }
}
</script>

<template>
  <div id="app" class="container">
    <h1>Lista de tareas</h1>
    <div v-if=" !estaEditando ">
      <input type="text" v-model=" tarea " />
      <button type="submit" @click=" guardarTarea ">Agregar</button>
    </div>
    <div v-else>
      <input type="text" v-model=" tarea " />
      <button type="submit" @click=" actualizarTarea ">Actualizar</button>
    </div>
    <ol>
      <li v-for="(  tarea, index  ) in   tareas  " :key=" index ">
        {{ tarea }}
        <button
          class="button button-outline"
          @click=" editarTarea( index, tarea ) "
        >Editar</button>
        <button class="button button-clear" @click=" eliminarTarea( index ) ">Eliminar</button>
      </li>
    </ol>
  </div>
</template>
