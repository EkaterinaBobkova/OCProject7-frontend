<template>
  <div class="container">
    <h1 class="title is-size-1">Merci de vous connecter :</h1>
    <div class="container">
      <p class="control has-icons-left has-icons-right">
        <input class="input" type="email" v-model="dataLogin.email" placeholder="Email" />
        <span class="icon is-small is-left">
          <i class="fas fa-envelope"></i>
        </span>
       
      </p>
    </div>

    <div class="container">
      <p class="control has-icons-left">
        <input class="input" type="password" v-model="dataLogin.password" placeholder="Password" />
        <span class="icon is-small is-left">
          <i class="fas fa-lock"></i>
        </span>
      </p>
    </div>
    <input @click.prevent="logIn" class="styled" type="submit" value="Envoyer" />
  </div>
</template>

<script>
import axios from "axios";
import { mapState } from "vuex";
export default {
  name: "Signin",
  data() {
    return {
      dataLogin: {
        email: null,
        password: null
      },
      msg: ""
    };
  },
  computed: {
    ...mapState(["user"])
  },
  methods: {
    logIn() {
      if (
        
        this.dataLogin.email !== null ||
        this.dataLogin.password !== null
      ) {
        axios
          .post("http://localhost:3000/api/auth/login", this.dataLogin)
          .then(response => {
            localStorage.setItem('token',response.data.token)
            location.replace(location.origin)
            
          })
          .catch(error => console.log(error));
      } else {
        console.log("Erreur est survenue !");
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
  background-image: linear-gradient(
    to top left,
    rgba(0, 0, 0, 0.2),
    rgba(0, 0, 0, 0.2) 30%,
    rgba(0, 0, 0, 0)
  );
  box-shadow: inset 2px 2px 3px rgba(255, 255, 255, 0.6),
    inset -2px -2px 3px rgba(0, 0, 0, 0.6);
}

.styled:hover {
  background-color: rgba(255, 0, 0, 1);
}
</style>