<template>
  <div class="home">
    <h1>This is the Homepage</h1>

    <div class="movie-list">
      <h2>Most Popular Movies of 2021</h2>

      <ul v-if="data">
        <li v-for="movie in data.results" :key="movie.id">
          <MovieCard :movie="movie" />
        </li>
      </ul>

      <p v-else>Chargement...</p>
    </div>
  </div>
</template>

<script>
import { ref, onMounted } from 'vue'
import MovieCard from '../components/MovieCard'

export default {
  name: 'Home',
  components: {
    MovieCard
  },
  setup () {
    const data = ref(null)

    onMounted(async () => {
      const endpoint = `https://api.themoviedb.org/3/discover/movie?primary_release_year=2021&sort_by=popularity.desc&api_key=${process.env.VUE_APP_API_KEY}`
      const response = await fetch(endpoint)
      data.value = await response.json()
    })

    return {
      data
    }
  }
}
</script>

<style lang="scss" scoped>
ul {
  display: grid;
  gap: 2rem;
  grid-template-columns: 1fr;
  margin-bottom: 10rem;

  @media screen and (min-width: 768px) {
    grid-template-columns: repeat(2, 1fr);
  }

  @media screen and (min-width: 1024px) {
    grid-template-columns: repeat(3, 1fr);
  }

  @media screen and (min-width: 1280px) {
    grid-template-columns: repeat(4, 1fr);
  }

}
</style>
