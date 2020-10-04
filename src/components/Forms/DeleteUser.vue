<template>
<div>
  <form @click.prevent="() => deleteAccount(form.id)" v-if="show">
    <h2 align="left">Suppression de votre compte :</h2>
    <p
      align="left"
     
    >Vous pouvez supprimer votre compte via le formulaire ci-dessous. </p>

    <div class="container">
      <p class="control has-icons-left">
        <input class="input" type="email"   label="Saisissez votre Email :" v-model="form.email"   placeholder="Validez votre email" pattern="^[a-z0-9._%+-]+@[a-z0-9.-]+\.[a-z]{2,}$"/>
        <span class="icon is-small is-left">
          <i class="fas fa-lock"></i>
        </span>
      </p>
    </div>

      <div class="container">
      <p class="control has-icons-left">
        <input class="input" type="password"   label="Saisissez votre mot de passe :"  v-model="form.password"  placeholder="Votre mot de passe">
        <span class="icon is-small is-left">
          <i class="fas fa-lock"></i>
        </span>
      </p>
    </div>
    

    

    <p >{{messageErreur}}</p>
    <p >{{message}}</p>
    <button class="button" type="submit" >Supprimer  mon compte</button>
  </form>
</div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      form: {
        id: JSON.parse(localStorage.getItem("id")),
        email: "",
        password: "",
      },
      props: ['userId', 'token'],
      show: true,
      message: "",
      messageErreur: "",
    };
    
  },
  methods: {
    deleteAccount() { 
       
      axios
        .delete("http://localhost:3000/api/auth/users/" + this.userId, {
          headers: {
            Authorization: "Bearer " + localStorage.getItem("token")
          }
        })
        .then(() => {
            this.message =
            "Votre compte à été correctement supprimé.";
          localStorage.clear();
          location.replace(location.origin+'/#/signup');
        })
        .catch(error => console.log(error));
      
    },
  }
}

</script>