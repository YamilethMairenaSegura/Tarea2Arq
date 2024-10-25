<template>
  <div>
    <h1>Modelos de Superdeportivos</h1>
    <ul>
      <li v-for="modelo in modelos" :key="modelo.id">
        <img :src="modelo.image" :alt="modelo.name">
        <h2>{{ modelo.name }}</h2>
        <p>País: {{ modelo.country }}</p>
        <p>Año de lanzamiento: {{ modelo.year }}</p>
        <p>Velocidad máxima: {{ modelo.topSpeed }} km/h</p>
        <router-link :to="`/fabricantes/${modelo.fabricante}`">
          Fabricante: {{ modelo.fabricante }}
        </router-link>
        <router-link :to="`/diseñadores/${modelo.diseñador}`">
          Diseñador: {{ modelo.diseñador }}
        </router-link>
      </li>
    </ul>

    <!-- Botón para regresar al Home -->
    <div class="back-home">
      <NuxtLink to="/">
        <button>Inicio</button>
      </NuxtLink>
    </div>

    <!-- Contenedor de comentarios de Utterances -->
    <div id="utterances-container" />
  </div>
</template>

<script>
export default {
  async asyncData () {
    try {
      // Cargar los datos desde el archivo estático modelos.json
      const modelos = await fetch('/data/modelos.json').then(res => res.json())
      return { modelos }
    } catch (error) {
      console.error('Error al cargar los modelos:', error)
      return { modelos: [] }
    }
  },
  mounted () {
    // Inyectar el script de Utterances cuando el componente esté montado
    const script = document.createElement('script')
    script.src = 'https://utteranc.es/client.js'
    script.async = true
    script.setAttribute('repo', 'YamilethMairenaSegura/Tarea2Utterances') // Nombre de tu repo
    script.setAttribute('issue-term', 'pathname')
    script.setAttribute('theme', 'github-light')
    script.setAttribute('crossorigin', 'anonymous')
    const commentBox = document.getElementById('utterances-container')
    if (commentBox) {
      commentBox.appendChild(script)
    }
  }
}
</script>

<style scoped>
/* El mismo estilo que tienes en tu código actual */
a {
  color: black;
}
.back-home {
  display: flex;
  justify-content: flex-start;
  padding: 10px;
  position: fixed;
  top: 0;
  left: 0;
  z-index: 1000;
  background-color: white;
  width: 100%;
}
.container {
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
}
ul {
  list-style: none;
  padding: 0;
  margin: 0;
}
li {
  margin: 20px 0;
  border: 1px solid #ddd;
  padding: 20px;
  border-radius: 5px;
  background-color: #f9f9f9;
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
}
img {
  width: 900px;
  height: auto;
  margin-bottom: 10px;
}
h2, p {
  color: black;
}
.links {
  display: flex;
  gap: 50px;
  justify-content: center;
}
.link {
  color: red;
  text-decoration: none;
}
.link:hover {
  text-decoration: underline;
}
</style>
