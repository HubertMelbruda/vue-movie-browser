<template>
  <div class="movie">
    <h1 class="movie__title">{{ movie.Title }}</h1>
    <div class="movie__details">
      <img class="movie__img" :src="movie.Poster" alt="Movie poster" />
      <div class="movie__description">
        <p class="movie__description--detail">
          <span class="bold">Year:</span> {{ movie.Year }}
        </p>
        <p class="movie__description--detail">
          <span class="bold">Director:</span> {{ movie.Director }}
        </p>
        <p class="movie__description--detail">
          <span class="bold">Language:</span> {{ movie.Language }}
        </p>
        <p class="movie__description--detail">
          <span class="bold">Released:</span> {{ movie.Released }}
        </p>
        <p class="movie__description--detail">
          <span class="bold">Run Time:</span> {{ movie.Runtime }}
        </p>
        <p class="movie__description--detail">
          <span class="bold">Type:</span> {{ movie.Type }}
        </p>
        <p class="movie__description--detail">
          <span class="bold">IMDb:</span> {{ movie.imdbRating }}
        </p>
      </div>
    </div>
    <div class="plot">
      <p>{{ movie.Plot }}</p>
    </div>
  </div>
</template>

<script>
import { ref, onBeforeMount } from "vue"
import { useRoute } from "vue-router"
const axios = require("axios").default

export default {
  setup() {
    const movie = ref({})
    const route = useRoute()

    onBeforeMount(() => {
      axios
        .get(
          `http://www.omdbapi.com/?apikey=e50d118f&i=${route.params.id}&plot=full`
        )
        .then(res => {
          movie.value = res.data
        })
    })
    return { movie }
  },
}
</script>

<style lang="scss" scoped>
.movie {
  background: #2c3d4e;
  padding: 20px;
  margin: 20px 0;
  border-radius: 10px;
  box-shadow: 0px 0px 10px #ffffff;
}

.movie__title {
  color: #f0f0f0;
  text-align: center;
  margin-bottom: 20px;
  font-family: "Roboto";
}

.movie__details {
  display: flex;
  flex-wrap: wrap;
}

.movie__img {
  border-radius: 10px;
  margin: 0 auto;
}

.movie__description {
  display: flex;
  flex-direction: column;
  color: #f0f0f0;
  padding: 20px 40px;
  margin: 0 auto 0 0;
}

.movie__description--detail {
  max-width: 450px;
  padding: 5px;
  font-size: 19px;
}

.bold {
  font-weight: 600;
}

.plot {
  color: #f0f0f0;
  font-size: 25px;
  padding: 20px;
}
</style>
