<template>
  <div class="home">
    <div class="feature-card">
      <router-link to="/movie/tt0409591">
        <img src="https://i.pinimg.com/564x/2a/2f/08/2a2f0865435e49294f00aeaae4ca9a2f.jpg" alt="Blade Runner" class="featured-img">
        <div class="detail">
          <h3>Blade Runner</h3>
          <p>Young Blade Runner K's discovery of a long-buried secret leads him to track down former Blade Runner Rick Deckard, who's been missing for thirty years.</p>
        </div>
      </router-link>
    </div>
    <form @submit.prevent class="search-box">
      <input type="text" placeholder="What movie do you want to watch?">
      <input type="submit" value="Search" class="search">
    </form>

    <div class="movies-list">MOVIES</div>
  </div>
</template>

<script>


export default {
 
}
</script>

<style lang="scss" scoped>
  .home {
    .feature-card {
      position: relative;

      .featured-img {
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

        h3 {
          color:#FFF;
          margin-bottom: 16px;
        }

        p {
          color: #FFF;
        }
      }
    }
  }

  .search-box {
    display: flex;
    justify-content: center;
    align-content: center;
    align-items: center;

  }
</style>