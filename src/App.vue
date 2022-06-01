<template>
  <header class="header">
    <router-link to="/">
      <h1 class="header__logo">
        <span class="header-logo__first-part">Vue</span>Movies
      </h1>
    </router-link>
  </header>
  <main>
    <router-view />
  </main>
  <!-- <footer>
      
  </footer> -->
</template>

<script>
export default {}
</script>

<style lang="scss">
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: "Quicksand", "Roboto", sans-serif;

  &::selection {
    background: transparentize($color: #42b883, $amount: 0.5);
  }
}

body {
  margin: 0 auto;
  background-color: #35495e;
  min-width: 600px;
  max-width: 900px;
}

a {
  text-decoration: none;
}

.header {
  display: flex;
  align-content: center;
  justify-content: center;
  background-color: #2c3d4e;
  padding: 10px 16px;
  margin: 10px 0;
  border-radius: 10px;
  box-shadow: 0px 0px 10px #ffffff;
}

.header__logo {
  color: #fff;
  font-size: 28px;

  .header-logo__first-part {
    color: #42b883;
  }
}

@media (max-width: 600px) {
  body {
    min-width: 300px;
  }
}
</style>
