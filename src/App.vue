<script >
import { ref } from 'vue'

export default {
  setup() {
    const estaEditando = ref( false );
    const tarea = ref( "" );
    const tareas = ref( [] );
    const tareaSeleccionada = ref( null );

    function guardarTarea() {
      if ( tarea.value.trim() === "" ) {
        return;
      }
      tareas.value.push( tarea );
     // tarea.value = "";
    }

    function eliminarTarea( index ) {
      tareas.value.splice( index, 1 );
    }

    function actualizarTarea( index ) {
      tareas.value.splice( index, 1, tarea );
      estaEditando.value = false;
      tarea.value = "";
    }

    function editarTarea( index, tarea ) {
      estaEditando.value = true;
      tarea.value = tarea
      tareaSeleccionada.value = index;
      // selectedIndex = index;
    }

    return {
      // properties that the template needs should be returned here
      estaEditando,
      tarea,
      tareas,
      tareaSeleccionada,
      guardarTarea,
      eliminarTarea,
      actualizarTarea,
      editarTarea
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
      <button type="submit" selected index="index" @click=" actualizarTarea( index ) ">Actualizar</button>
    </div>
    <ol>
      <li v-for = "( tarea, index) in  tareas" :key=" index ">
        {{ tarea }}
        <button
          class="button button-outline"
          @click=" editarTarea( index, tarea ) "
          selected
          index="{{ index }}"
        >Editar</button>
        <button class="button button-clear" @click=" eliminarTarea( index ) ">Eliminar</button>
      </li>
    </ol>
  </div>
</template>

<style  scoped>
</style>