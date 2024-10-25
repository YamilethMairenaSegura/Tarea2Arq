<template>
  <div class="designer-page">
    <h1>Diseñadores de Superdeportivos</h1>

    <!-- Lista de diseñadores -->
    <ul class="designer-list">
      <li v-for="diseñador in diseñadores" :key="diseñador.id" class="designer-item">
        <img :src="diseñador.image" :alt="diseñador.name" class="designer-image">
        <h2>{{ diseñador.name }}</h2>
        <p>Nacionalidad: {{ diseñador.nationality }}</p>
        <p>Obras destacadas: {{ diseñador.notableWorks }}</p>

        <!-- Enlaces a los modelos y fabricantes -->
        <div class="links">
          <router-link :to="`/modelos/${diseñador.modeloId}`" class="link">
            Modelos
          </router-link>
          <router-link :to="`/fabricantes/${diseñador.fabricanteId}`" class="link">
            Fabricantes
          </router-link>
        </div>
      </li>
    </ul>

    <!-- Contenedor de comentarios de Utterances -->
    <div id="utterances-container" />

    <!-- Botón para regresar a la página de inicio -->
    <button class="btn-home" @click="goHome">
      Inicio
    </button>
  </div>
</template>

<script>
export default {
  async asyncData () {
    const diseñadores = await fetch('/data/diseñadores.json').then(res => res.json())
    return { diseñadores }
  },
  mounted () {
    // Inyectar el script de Utterances
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
  },
  methods: {
    goHome () {
      this.$router.push('/')
    }
  }
}
</script>

<style scoped>
/* Contenedor principal de la página */
.designer-page {
  text-align: center;
  padding: 20px;
}

/* Lista de diseñadores */
.designer-list {
  list-style-type: none;
  padding: 0;
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
}

/* Cada ítem de la lista */
.designer-item {
  margin: 20px;
  width: 300px;
  background-color: #f9f9f9;
  padding: 20px;
  border-radius: 10px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  text-align: center;
}

/* Imagen del diseñador centrada */
.designer-image {
  max-width: 100%;
  height: auto;
  margin: 0 auto 10px;
  border-radius: 10px;
}

/* Estilo de los enlaces */
.links {
  margin-top: 10px;
}

.links .link {
  margin: 0 10px;
  text-decoration: none;
  color: #007bff;
}

.links .link:hover {
  text-decoration: underline;
}

/* Botón para regresar a Home */
.btn-home {
  margin-top: 20px;
  padding: 10px 20px;
  background-color: #007bff;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

.btn-home:hover {
  background-color: #0056b3;
}
</style>
