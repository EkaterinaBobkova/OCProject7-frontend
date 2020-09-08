<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png">
    <Connection msg="Connection à l'application"/>
  </div>
</template>

<script>
// @ is an alias to /src
import Connection from '@/components/Connection.vue'

export default {
  name: 'Home',
  components: {
    Connection
  }
}
</script>
