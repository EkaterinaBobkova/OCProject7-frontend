<template>
  <nav class="navbar" role="navigation" aria-label="main navigation">
    <div class="navbar-brand">
      <a class="navbar-item" href="/">
        <a href="#"
          ><img
            id="logo"
            src="@/assets/logo.png"
            width="250"
            height="400"
            alt="logo"
        /></a>
      </a>
    </div>

    <div id="navbar" class="navbar-menu">
      <div class="navbar-start">
        <router-link to="/" class="navbar-item">Accueil</router-link>
        <router-link to="/about" class="navbar-item">A propos</router-link>
        <router-link to="/wall" class="navbar-item"
          >Voir les publications</router-link
        >
      </div>
      <div class="navbar-end">
        <div class="navbar-item">
          <div class="buttons">
            <a class="button is-dark">
              <router-link to="/signin" class="navbar-item"
                >Sign in</router-link
              >
            </a>
            <a class="button is-dark">
              <router-link to="/signup" class="navbar-item"
                >Sign up</router-link
              >
            </a>
            <a class="button is-dark">
              <router-link to="/user" class="navbar-item"
                >Votre compte</router-link
              >
            </a>
          </div>
        </div>
      </div>
    </div>
  </nav>
</template>
<script>
export default {
  name: "Nav",
};
</script>
<style lang="scss" scoped>
.navbar {
  background-color: #122442;
  height: 120px;
}

a {
  font-weight: bold;
  color: #ffff;
}

@media screen and (max-width: 1000px) {
  #navbar {
    display: flex;

    background-color: #122442;
    height: 190px;
  }
}
</style>