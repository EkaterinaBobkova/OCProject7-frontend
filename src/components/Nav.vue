<template>
<nav class="navbar container" role="navigation" aria-label="main navigation">
  <div class="navbar-brand">
    <a class="navbar-item" href="/">
     <a href="#"><img id="logo" src="@/assets/logo.png" width="250" height="500" alt="logo"/></a>
    </a>
    <a role="button" class="navbar-burger burger" aria-label="menu" aria-expanded="false" data-target="navbarBasicExample">
      <span aria-hidden="true"></span>
      <span aria-hidden="true"></span>
      <span aria-hidden="true"></span>
    </a>
  </div>
  <div id="navbar" class="navbar-menu">
    <div class="navbar-start">
      <router-link to="/" class="navbar-item">Accueil</router-link>
      <router-link to="/about" class="navbar-item">A propos</router-link>
      <router-link to="/wall" class="navbar-item">Voir les publications</router-link>
    </div>
    <div class="navbar-end">
      <div class="navbar-item">
        <div class="buttons">
           <a class="button is-light">
            <router-link to="/signin" class="navbar-item">Sign in</router-link>
          </a>
          <a class="button is-light">
            <router-link to="/signup" class="navbar-item">Sign up</router-link>
          </a>
            <a class="button is-light">
            <router-link to="/user" class="navbar-item">Votre compte</router-link>
          </a>
        </div>
      </div>
    </div>
  </div>
</nav>
</template>
<script>
export default {
    name: 'Nav'
}
</script>
<style lang="scss" scoped>
  nav {
    margin-top: 25px;
    margin-bottom: 30px;
  
    a {
      font-weight: bold;
      color: #363738;
      &.router-link-exact-active {
        color: #c91010;
      }
    } 
  
  } 



</style>