<template>
  <div class="movie-detail-page">
    <RouterLink to="/" class="go-back-link">Go Back</RouterLink>

    <p v-if="!movie">Chargement...</p>

    <div class="movie-content" v-if="movie && movie.id">
      <div class="movie-cover">
        <img :src="`https://image.tmdb.org/t/p/w300/${movie.poster_path}`" :alt="`Cover du film ${movie.title}`">
      </div>

      <div class="movie-details">
        <h1>{{ movie.title }}</h1>
        <ul>
          <li><p>{{ movie.overview }}</p></li>
          <li><strong>Score:</strong> {{ movie.vote_average }}/10 ({{ movie.vote_count }} votes)</li>
          <li><strong>Release date:</strong> {{ formattedDate }}</li>
          <li class="genres">
            <strong class="genres">Genres:</strong>
            <ul>
              <li v-for="genre in movie.genres" :key="genre.id">
                {{ genre.name }}
              </li>
            </ul>
          </li>
        </ul>
      </div>
    </div>

    <p v-if="movie && !movie.id">Il n'y pas de film avec l'id: {{id}}</p>
  </div>
</template>

<script>
import { computed, onMounted, ref } from 'vue'
import { useRoute } from 'vue-router'

export default {
  name: 'About',
  components: {
  },
  setup () {
    const route = useRoute()
    const id = route.params.id

    const movie = ref(null)

    const formattedDate = computed(() => {
      if (!movie.value) { return null }

      const date = new Date(movie.value.release_date)
      return date.toLocaleString('fr', { day: '2-digit', month: '2-digit', year: '2-digit' })
    })

    onMounted(async () => {
      const endpoint = `https://api.themoviedb.org/3/movie/${id}
        ?api_key=${process.env.VUE_APP_API_KEY}`
      const response = await fetch(endpoint)
      movie.value = await response.json()
    })

    return {
      id,
      movie,
      formattedDate
    }
  }
}
</script>

<style lang="scss" scoped>
.go-back-link {
  font-size: 2.8rem;
  font-weight: bold;
}

.movie-detail-page {
  margin-top: 2rem;

  .movie-content {
    margin-top: 2rem;
    display: grid;
    gap: 2rem;
    grid-template-columns: 1fr 3fr;
  }
  .movie-cover {
    border-radius: 0.5rem;
    overflow: hidden;
  }

  .genres {
    display: flex;
    ul {
      margin-left: 1ch;
      display: flex;

      li {
        &::before { content: '\00a0'; }
        &:not(:last-child)::after { content: ' -'; }
      }
    }
  }
}

</style>
