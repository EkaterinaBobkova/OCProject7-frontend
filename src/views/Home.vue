<template>
<div class="home">
  <section class="general">
    <div class="general-body">
      <div class="container">
        <h1 class="title">
          Bienvenue sur le réseau social Groupomania !       
        </h1>
        <h2 class="subtitle">
          Partagez vos émotions avec vos collegues
        </h2>
       
      </div>
    </div>
  </section>
</div>
</template>
<script>
export default {
  name: 'home',
  components: {
  }
}
</script>
<style lang="scss" scoped>
  .general {    
    text-align: center;
    background-image: url(../assets/banner.jpg);
    background-size: cover;
    background-position: center;
    background-repeat: no-repeat;
    height: 400px;
  }
  .general-body .title {
    color: white;
    text-shadow: 4px 4px 4px rgba(49, 46, 46, 0.6);
    padding: 40px 0 20px 0;
    font-size: 60px;
  }
  .subtitle {
   color: white;
   text-shadow: 4px 4px 4px rgba(49, 46, 46, 0.6);
    font-size: 30px;
  }
  .button-block {
    text-align: center;
    margin-left: auto;
    margin-right: auto;
    width: 100%;
    position: absolute;
    bottom: -150px;
    .button {
      margin-right: 50px;
      padding-left: 50px;
      padding-right: 50px;
    }
    .welcome {
      width: 400px;
      padding: 10px;
      margin-left: auto;
      margin-right: auto;
    }
  }
  .is-xl {
    font-size: 1.7rem;
  }
</style>