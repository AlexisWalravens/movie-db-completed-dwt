<template>
  <div class="movie-card">
    <RouterLink :to="`/movie/${id}`">
      <figure>
        <img :src="`https://image.tmdb.org/t/p/w300/${poster}`" :alt="`Cover du film ${title}`">
        <figcaption>
          <ul>
            <li><strong class="title">{{ title }}</strong></li>
            <li><span class="score">Score: {{ score }}/10</span></li>
          </ul>
        </figcaption>
      </figure>
    </RouterLink>
  </div>
</template>

<script>
export default {
  props: {
    id: {
      type: Number,
      required: true
    },
    score: {
      type: Number,
      required: true
    },
    title: {
      type: String,
      required: true
    },
    poster: {
      type: String,
      required: true
    }
  },
  setup () {
    return {}
  }
}
</script>

<style lang="scss" scoped>
.movie-card {
  border-radius: 0.5rem;
  box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1), 0 2px 4px -1px rgba(0, 0, 0, 0.06);
  overflow: hidden;
  width: 100%;
  height: 100%;
  transition: transform .3s ease-out;

  &:hover {
    transform: scale(1.05);
  }

  a {
    color: black;
    text-decoration: none;
  }

  figure {
    margin: 0;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    height: 100%;
  }
  figcaption {
    padding: 2rem;
  }

  .title {
    font-size: 1.8rem;
  }
}
</style>
