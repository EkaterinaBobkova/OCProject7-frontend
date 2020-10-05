<template>
  <div id="app">
    <Nav />
    <router-view/>
    
     <Footer />
  </div>
</template>
<script>
import Nav from '@/components/Nav.vue';
import Footer from '@/components/Footer.vue';

export default {
  name: 'app',
  components: {
    Nav,
    Footer
  }  
}
</script>
<style lang="scss">
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
</style>
