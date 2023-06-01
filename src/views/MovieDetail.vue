<template>
  <div class="movie-detail">
    <h2>{{ movie.Title }}</h2>
    <p>{{ movie.Year }}</p>
    <img :src="movie.Poster" alt="Movie Poster" class="featured-img" />
    <p>{{ movie.Plot }}</p>
  </div>
</template>

<script>
import { ref, onMounted } from 'vue'
import { useRoute } from 'vue-router'
import axios from 'axios'

export default {
  setup() {
    const movie = ref({})
    const route = useRoute()

    const { VITE_MOVIE_URL_BASE, VITE_MOVIE_API_KEY } = import.meta.env

    onMounted(async () => {
      await axios
        .get(`${VITE_MOVIE_URL_BASE}${VITE_MOVIE_API_KEY}&i=${route.params.id}&plot=full`)
        .then((response) => {
          movie.value = response.data
        })
        .catch((e) => {
          this.errors.push(e)
        })
    })

    return {
      movie
    }
  }
}
</script>

<style lang="scss">
.movie-detail {
  padding: 16px;

  h2 {
    color: #fff;
    font-size: 28px;
    font-weight: 600;
    margin-bottom: 16px;
  }

  .featured-img {
    display: block;
    max-width: 200px;
    margin-bottom: 16px;
  }

  p {
    color: #fff;
    font-size: 18px;
    line-height: 1.4;
  }
}
</style>
