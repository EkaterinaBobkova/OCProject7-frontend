<template>

 <div class="container">
          <h1 class="title is-size-1">Pour créer votre profil</h1>          
      

      <div class="container">
     
  <p class="control has-icons-left has-icons-right">
    <input class="input" type="username" placeholder="Username">
    <span class="icon is-small is-left">
      <i class="fas fa-user"></i>
      
    </span>
    <span class="icon is-small is-right">
      <i class="fas fa-check"></i>
    </span>
  </p>
</div>
 <div class="container">
     
  <p class="control has-icons-left has-icons-right">
    <input class="input" type="email" placeholder="Email">
    <span class="icon is-small is-left">
      <i class="fas fa-envelope"></i>
    </span>
    <span class="icon is-small is-right">
      <i class="fas fa-check"></i>
    </span>
  </p>
</div>
<div class="container">
  <p class="control has-icons-left">
    <input class="input" type="password" placeholder="Password">
    <span class="icon is-small is-left">
      <i class="fas fa-lock"></i>
    </span>
  </p>
</div>
  </div>
</template>

<script>


export default {
  name: 'Signup',
  components: {
    
  },
}
</script>