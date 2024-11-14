<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <h3>Añadir tarea</h3> 
    <p>Permite al usuario ingresar tareas de forma manual.</p>
    <h3>Lista de tareas</h3>
    <p>Incluye un botón que, al ser presionado, obtiene tareas desde la API.</p>
    <h3>Vistas combinadas</h3>
    <p>Esta sección extrae automáticamente las tareas de la API y permite agregar nuevas tareas al mismo tiempo</p>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
