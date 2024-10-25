<template>
  <div class="container">
    <h1>Bienvenido al Catálogo de Superdeportivos</h1>
    <p>Explora los diferentes modelos, fabricantes, y diseñadores de autos superdeportivos.</p>
    <ul>
      <li>
        <NuxtLink to="/modelos">Modelos</NuxtLink>
      </li>
      <li>
        <NuxtLink to="/fabricantes">Fabricantes</NuxtLink>
      </li>
      <li>
        <NuxtLink to="/diseñadores">Diseñadores</NuxtLink>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  head() {
    return {
      title: 'Catálogo de Superdeportivos - Inicio'
    }
  }
}
</script>

<style>
html, body {
  margin: 0;
  padding: 0;
  height: 100%;
}

.container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 100vh; /* Asegura que el contenedor cubra toda la pantalla */
  width: 550vw; /* Asegura que el contenedor tenga todo el ancho de la pantalla */
  background-image: url('/images/Ferrari_F8_Tributo.jpg');
  background-size: cover; /* La imagen cubrirá todo el contenedor */
  background-position: center;
  background-repeat: no-repeat; /* Evita que la imagen se repita */
  color: #fff;
  text-align: center;
  padding: 0;
}

h1 {
  font-size: 4em;
  color: #fff;
}

p {
  font-size: 1.5em;
}

ul {
  list-style: none;
  padding: 0;
}

li {
  margin: 10px 0;
}

a {
  color: #e2d9d9;
  text-decoration: none;
  font-size: 2.2em;
}

a:hover {
  text-decoration: underline;
}
</style>