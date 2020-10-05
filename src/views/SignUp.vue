<template>

 <div class="container">
          <h1 class="title is-size-1">Pour créer votre profil :</h1>          
      

      <div class="container">
     
  <p class="control has-icons-left has-icons-right">
    <input class="input" type="username" v-model="dataSignup.username" placeholder="Username">
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
    <input class="input" type="email"  v-model="dataSignup.email" placeholder="Email">
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
    <input class="input" type="password" v-model="dataSignup.password" placeholder="Password">
    <span class="icon is-small is-left">
      <i class="fas fa-lock"></i>
    </span>
  </p>
</div>
<input @click.prevent="sendSignup" class="styled"
       type="submit"
       value="Envoyer">

  </div>
</template>

<script>


import axios from "axios";

export default {
  name: "Signup",
  data() {
    return {
      dataSignup: {
        username: null,
        email: null,
        password: null
      },
      msg: ""
    };
  },
 
  methods: {
    sendSignup() {
      const regexPassword = /^(?=.*[A-Z])(?=.*[a-z])(?=.*\d)(?=.*[-+!*$@%_])([-+!*$@%_\w]{8,15})$/




      const regexEmail = /^[a-z0-9!#$ %& '*+/=?^_`{|}~-]+(?:\.[a-z0-9!#$%&' * +/=?^_`{|}~-]+)*@(?:[a-z0-9](?:[a-z0-9-]*[a-z0-9])?\.)+[a-z0-9](?:[a-z0-9-]*[a-z0-9])?$/g;
     
      if (
        (this.dataSignup.email !== null ||
        this.dataSignup.username !== null ||
        this.dataSignup.password !== null) &&
        regexPassword.test(this.dataSignup.password) && regexEmail.test(this.dataSignup.email) && this.dataSignup.username
      ) {
        axios
          .post("http://localhost:3000/api/auth/signup", this.dataSignup)
          .then(response => {
            console.log(response);
           
            // this.dataSignup.email = null;
            // this.dataSignup.username = null;
            // this.dataSignup.password = null;
        location.replace(location.origin)
          })
          .catch(error => console.log(error));
      } else {
        alert("Le mot de passe doit contenir de 8 à 15 caractères,au moins une lettre minuscule, une lettre majuscule, un chiffre et un de ces caractères spéciaux: $ @ % * + - _ !");
      }
    }
  }
};
</script>

<style lang="scss" scoped>
  


.styled {
    border: 0;
    line-height: 2.5;
    padding: 0 20px;
    margin-top: 20px;
    font-size: 1rem;
    text-align: center;
    color: #fff;
    text-shadow: 1px 1px 1px #000;
    border-radius: 10px;
    background-color: rgba(220, 0, 0, 1);
    background-image: linear-gradient(to top left,
                                      rgba(0, 0, 0, .2),
                                      rgba(0, 0, 0, .2) 30%,
                                      rgba(0, 0, 0, 0));
    box-shadow: inset 2px 2px 3px rgba(255, 255, 255, .6),
                inset -2px -2px 3px rgba(0, 0, 0, .6);
}

.styled:hover {
    background-color: rgba(255, 0, 0, 1);
}
    </style>