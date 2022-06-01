<template>
  <div class="home">
    <div class="feature-card">
      <router-link to="/movie/tt0409591">
        <img
          src="https://i.pinimg.com/564x/2a/2f/08/2a2f0865435e49294f00aeaae4ca9a2f.jpg"
          alt="Blade Runner"
          class="feature-card__img"
        />
        <div class="detail">
          <h3 class="detail__header">Blade Runner</h3>
          <p class="detail__info">
            Young Blade Runner K's discovery of a long-buried secret leads him
            to track down former Blade Runner Rick Deckard, who's been missing
            for thirty years.
          </p>
        </div>
      </router-link>
    </div>
    <form @submit.prevent="searchMovies" class="search-box">
      <input
        type="text"
        placeholder="What movie do you want to watch?"
        class="search-box__input search-box--reset"
        v-model="search"
      />
      <!-- <input type="submit" value="Search" class="search-button"> -->
      <button type="submit" class="search-box__search-btn search-box--reset">
        Search
      </button>
    </form>

    <div class="movies-list" v-if="movies.length">
      <div class="movies-list__header">Movies</div>
      <div class="movies-list__container">
        <div class="movie-card" v-for="movie in movies" :key="movie.imdbID">
          <router-link
            :to="{ name: 'Movie Detail', params: { id: movie.imdbID } }"
          >
            <div class="movie-card__img">
              <img :src="movie.Poster" alt="movie poster" />
              <p class="movie-card__movie-type">{{ movie.Type }}</p>
            </div>
            <div class="movie-card__details">
              <h3 class="movie-card__title">{{ movie.Title }}</h3>
              <p>{{ movie.Year }}</p>
            </div>
          </router-link>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { ref } from "vue"
const axios = require("axios").default

export default {
  setup() {
    const search = ref("")
    const movies = ref([])
    const error = ref(null)

    const searchMovies = () => {
      if (search.value !== "") {
        axios
          .get(`http://www.omdbapi.com/?apikey=e50d118f&s=${search.value}`)
          .then(res => {
            movies.value = res.data.Search
            search.value = ""
          })
          .catch(err => (error.value = err))
      }
    }

    return { search, movies, searchMovies }
  },
}
</script>

<style lang="scss" scoped>
.feature-card {
  position: relative;
  border-radius: 10px;
}

.feature-card__img {
  display: block;
  width: 100%;
  height: 300px;
  object-fit: cover;
  position: relative;
  z-index: 0;
  border-radius: 10px;
}

.detail {
  position: absolute;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: rgba(0, 0, 0, 0.6);
  border-radius: 10px;
  padding: 16px;
  z-index: 1;
}

.detail__header {
  color: #fff;
  margin-bottom: 16px;
}

.detail__info {
  color: #fff;
}

.search-box {
  display: flex;
  flex-direction: column;
  align-content: center;
  align-items: center;
  padding: 10px 15px;
}

.search-box--reset {
  display: block;
  appearance: none;
  border: none;
  outline: none;
  background: none;
}

.search-box__input {
  width: 100%;
  color: #fff;
  background-color: #496583;
  text-align: center;
  font-size: 18px;
  padding: 10px 20px;
  border-radius: 15px;

  &::placeholder {
    color: rgb(200, 200, 200);
  }

  &:focus {
    box-shadow: 0px 0px 10px #fff;
  }
}

.search-box__search-btn {
  width: 100%;
  max-width: 200px;
  color: #fff;
  font-size: 20px;
  background-color: #09a650;
  padding: 10px 15px;
  margin: 10px 10px 5px 10px;
  border-radius: 15px;

  &:active {
    background-color: #0bda68;
    box-shadow: 0px 0px 10px #0bda68;
  }
}

.movies-list {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.movies-list__header {
  font-size: 20px;
  color: #fff;
  text-align: center;
  background-color: #496583;
  padding: 5px 25px;
  margin-top: 20px;
  border-radius: 15px;
  width: 100%;
}

.movies-list__container {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-around;
  padding: 10px;
  margin: 10px;
}

.movie-card {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 10px;
  margin: 10px;
  background: #496583;
  border-radius: 15px;
  min-width: 300px;
}

.movie-card__img {
  overflow: hidden;
  position: relative;
  
  img {
    display: block;
    min-width: 280px;
    max-height: 400px;
    // aspect-ratio:  9 / 16;
    border-radius: 15px;
    object-fit: cover;
  }
}

.movie-card__movie-type {
  position: absolute;
  background: #09a650;
  font-size: 20px;
  color: #f0f0f0;
  padding: 5px;
  top: 350px;
  left: 0px;
  border-top-right-radius: 10px;
  border-bottom-right-radius: 10px;
}

.movie-card__details {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin: 10px;
  color: #f0f0f0;
  max-width: 300px;
}

@media (max-width: 450px) {
  .search-box__input {
    &::placeholder {
      font-size: 14px;
    }
  }
}
</style>
