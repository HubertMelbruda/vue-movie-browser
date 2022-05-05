<template>
  <div class="home">
    <div class="feature-card">
      <router-link to="/movie/tt0409591">
        <img src="https://i.pinimg.com/564x/2a/2f/08/2a2f0865435e49294f00aeaae4ca9a2f.jpg" alt="Blade Runner" class="feature-card__img">
        <div class="detail">
          <h3 class="detail__header">Blade Runner</h3>
          <p class="detail__info">Young Blade Runner K's discovery of a long-buried secret leads him to track down former Blade Runner Rick Deckard, who's been missing for thirty years.</p>
        </div>
      </router-link>
    </div>
    <form @submit.prevent="searchMovies" class="search-box">
      <input type="text" placeholder="What movie do you want to watch?" class="search-box__input search-box--reset" v-model="search" >
      <!-- <input type="submit" value="Search" class="search-button"> -->
      <button type="submit" class="search-box__button search-box--reset">Search</button>
    </form>

    <div class="movies-list">MOVIES</div>
  </div>
</template>

<script>
import { ref } from 'vue';

//e50d118f
// .then(response => response.json())


export default {
  setup() {
    const search = ref("")
    const movies = ref([])
    const error = ref(null)

      const searchMovies = () => {
        if(search.value !== "") {
          fetch(`http://www.omdbapi.com/?apikey=e50d118f&s=${search.value}`)
          .then(res => {
            if(!res.ok) {
              throw Error("There is a problem with data fetching.")
            }
            return res.json()
          })
          .then(data => {
            movies.value = data
            console.log(data)
          })
          .catch(err => error.value = err )
        }
      }
    return { search, movies, searchMovies }
  }
}
</script>

<style lang="scss" scoped>
  .home {
    .feature-card {
      position: relative;

      .feature-card__img {
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

        .detail__header {
          color:#fff;
          margin-bottom: 16px;
        }

        .detail__info {
          color: #fff;
        }
      }
    }
  }

  .search-box {
    display: flex;
    flex-direction: column;;

    align-content: center;
    align-items: center;
    padding: 15px;

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
        box-shadow: 0px 0px 10px #fff ;
      }
    }

    .search-box__button {
      width: 100%;
      max-width: 200px;
      color: #fff;
      font-size: 20px;
      background-color: #09a650;
      padding: 10px 15px;
      margin: 10px;
      border-radius: 15px;

      &:active {
        background-color: #0bda68;
        box-shadow: 0px 0px 10px #0bda68 ;
      }
    }
  }
</style>