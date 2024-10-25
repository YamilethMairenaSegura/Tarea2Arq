<template>
  <div class="fabricantes-page">
    <h1>Fabricantes de Superdeportivos</h1>

    <!-- Lista de fabricantes -->
    <ul class="fabricante-list">
      <li v-for="fabricante in fabricantes" :key="fabricante.id" class="fabricante-item">
        <img :src="fabricante.image" :alt="fabricante.name" class="fabricante-image">
        <h2>{{ fabricante.name }}</h2>
        <p>País: {{ fabricante.country }}</p>
        <p>Año de fundación: {{ fabricante.founded }}</p>

        <!-- Información de los modelos del fabricante -->
        <h3>fabricantes</h3>
        <ul v-if="fabricante.modelos" class="modelo-list">
          <li v-for="modelo in fabricante.modelos" :key="modelo.id" class="modelo-item">
            <img :src="modelo.image" :alt="modelo.name" class="modelo-image">
            <h2>{{ modelo.name }}</h2>
            <p>País: {{ modelo.country }}</p>
            <p>Año de lanzamiento: {{ modelo.year }}</p>
            <p>Velocidad máxima: {{ modelo.topSpeed }} km/h</p>
            <!-- Enlaces a fabricante y diseñador del modelo -->
            <router-link :to="`/fabricantes/${modelo.fabricante}`" class="link">
              Fabricante: {{ modelo.fabricante }}
            </router-link>
            <router-link :to="`/diseñadores/${modelo.diseñador}`" class="link">
              Diseñador: {{ modelo.diseñador }}
            </router-link>
          </li>
        </ul>

        <!-- Enlaces a los modelos y diseñadores -->
        <div class="links">
          <router-link :to="`/modelos/${fabricante.modeloId}`" class="link">
            Modelos
          </router-link>
          <router-link :to="`/diseñadores/${fabricante.diseñadorId}`" class="link">
            Diseñadores
          </router-link>
        </div>
      </li>
    </ul>

    <!-- Botón para regresar a la página de inicio -->
    <button class="btn-home" @click="goHome">
      Inicio
    </button>

    <!-- Contenedor de comentarios de Utterances -->
    <div id="utterances-container" />
  </div>
</template>

<script>
export default {
  async asyncData () {
    try {
      // Cargar datos de fabricantes y modelos
      const fabricantes = await fetch('/data/fabricantes.json').then(res => res.json())
      const modelos = await fetch('/data/modelos.json').then(res => res.json())

      // Asociar los modelos a sus respectivos fabricantes
      fabricantes.forEach((fabricante) => {
        fabricante.modelos = modelos.filter(modelo => modelo.fabricante === fabricante.name)
      })

      return { fabricantes }
    } catch (error) {
      console.error('Error al cargar los datos:', error)
      return { fabricantes: [] }
    }
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
.fabricante-page {
  text-align: center;
  padding: 20px;
}

/* Lista de fabricantes */
.fabricante-list {
  list-style-type: none;
  padding: 0;
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
}

/* Cada ítem de la lista */
.fabricante-item {
  margin: 20px;
  width: 300px;
  background-color: #f9f9f9;
  padding: 20px;
  border-radius: 10px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  text-align: center;
}

/* Imagen del fabricante con un tamaño consistente */
.fabricante-image {
  width: 335px;
  height: 350px;
  object-fit: cover;
  margin: 0 auto 20px;
  border-radius: 10px;
}

/* Lista de modelos */
.modelo-list {
  list-style-type: none;
  padding: 0;
  margin: 10px 0;
}

/* Cada ítem de modelo */
.modelo-item {
  margin: 10px 0;
  border: 1px solid #ddd;
  padding: 10px;
  border-radius: 5px;
  background-color: #f9f9f9;
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
}

.modelo-image {
  width: 200px;
  height: auto;
  margin-bottom: 10px;
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
