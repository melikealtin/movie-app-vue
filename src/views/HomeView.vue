<template>
  <div class="home">
    <div class="feature-card">
      <router-link to="/movie/tt0409591">
        <img
          src="https://i.pinimg.com/originals/f6/e8/c6/f6e8c64b1c0e337fc41d557cfe5797b6.jpg"
          alt="Naruto Poster"
          class="featured-image"
        />
        <div class="detail">
          <h3>Naruto</h3>
          <p>
            Naruto is a Japanese manga series written and illustrated by Masashi Kishimoto. It tells
            the story of Naruto Uzumaki, a young ninja who seeks recognition from his peers and
            dreams of becoming the Hokage, the leader of his village.
          </p>
        </div>
      </router-link>
    </div>

    <form @submit.prevent="SearchMovies()" class="search-box">
      <input type="text" placeholder="What are you looking for?" v-model="search" />
      <input type="submit" value="Search" />
    </form>

    <div class="movies-list">
      <div class="movie" v-for="movie in movies" :key="movie.imdbID">
        <router-link :to="'/movie/' + movie.imdbID" class="movie-link">
          <div class="product-image">
            <img :src="movie.Poster" alt="Movie Poster" />
            <div class="type">{{ movie.Type }}</div>
          </div>
          <div class="detail">
            <p class="year">{{ movie.Year }}</p>
            <h3>{{ movie.Title }}</h3>
          </div>
        </router-link>
      </div>
    </div>
  </div>
</template>

<script>
import { ref } from 'vue'
import axios from 'axios'

export default {
  setup() {
    const search = ref('')
    const movies = ref([])

    const { VITE_MOVIE_URL_BASE, VITE_MOVIE_API_KEY } = import.meta.env

    const SearchMovies = () => {
      if (search.value != '') {
        axios
          .get(`${VITE_MOVIE_URL_BASE}${VITE_MOVIE_API_KEY}&s=${search.value}`)
          .then((response) => {
            movies.value = response.data.Search
            search.value = ''
          })
          .catch((e) => {
            this.errors.push(e)
          })
      }
    }

    return {
      search,
      movies,
      SearchMovies
    }
  }
}
</script>

<style lang="scss">
.home {
  .feature-card {
    position: relative;

    .featured-image {
      display: block;
      width: 100%;
      height: 300px;
      object-fit: cover;
      position: relative;
      z-index: 0;
    }
    .detail {
      position: absolute;
      left: 0;
      right: 0;
      bottom: 0;
      background-color: rgba(0, 0, 0, 0.6);
      padding: 16px;
      z-index: 1;
    }
    h3 {
      color: #fff;
      margin-bottom: 16px;
    }
    p {
      color: #fff;
    }
  }
  .search-box {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    padding: 16px;

    input {
      display: block;
      appearance: none;
      border: none;
      outline: none;
      background: none;

      &[type='text'] {
        width: 100%;
        color: #fff;
        background-color: #2a2a42;
        font-size: 20px;
        padding: 10px 16px;
        border-radius: 8px;
        margin-bottom: 15px;
        transition: 0.4s;
        &::placeholder {
          color: #f3f3f3;
        }
        &:focus {
          box-shadow: 0px 3px 6px rgba(0, 0, 0, 0.4);
        }
      }
      &[type='submit'] {
        width: 100%;
        max-width: 300px;
        background-color: #786cd5;
        padding: 16px;
        border-radius: 8px;
        color: #fff;
        font-size: 20px;
        text-transform: uppercase;
        transition: 0.4s;
        &:active {
          background-color: darken(#786cd5, 10%);
        }
      }
    }
  }
  .movies-list {
    display: flex;
    flex-wrap: wrap;
    margin: 0px 8px;

    .movie {
      max-width: 50%;
      flex: 1 1 20%;
      padding: 16px 8px;

      .movie-link {
        display: flex;
        flex-direction: column;
        height: 100%;

        .product-image {
          position: relative;
          display: block;
          img {
            display: block;
            width: 100%;
            height: 370px;
            object-fit: cover;
          }
          .type {
            position: absolute;
            padding: 8px 16px;
            background-color: #ff7e9c;
            color: #fff;
            bottom: 16px;
            left: 0px;
            text-transform: capitalize;
          }
        }
        .detail {
          background-color: #6051d2;
          padding: 16px 8px;
          flex: 1 1 100%;
          border-radius: 0px 0px 8px 8px;

          .year {
            color: #aaa;
            font-size: 14px;
          }

          h3 {
            color: #fff;
            font-weight: 600;
            font-size: 18px;
          }
        }
      }
    }
  }
}
</style>
