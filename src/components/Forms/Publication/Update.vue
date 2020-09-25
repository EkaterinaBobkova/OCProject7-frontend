<template>
  <!--Creat a new post-->
  <div class="field">
    
    <div class="card">
       <textarea
            class="textarea"
            cols="55"
            rows="5"
             v-model="editedPost.content"
            placeholder="modifier le texte"
          ></textarea>
      
      <div v-if="message" class="alert alert-danger">{{ message }}</div>
       <input type="submit"  @click.prevent="() => editPost(editedPost.id)" class="button button is-dark" value="Envoyer" />
    </div>
   
   
  
  </div>
</template>
<script>
import axios from "axios";
export default {
  name: "Update",
  data() {
    return {
     
      editedPost: {
        content: "",
      },
      message: "",
      allPublications: [],
    };
    
  },
  methods: {
    editPost(id) {
        
      
        axios
          .put( "http://localhost:3000/api/publications/" + id,
            {
              
              content: this.editedPost.content,
           
            },
            {
              headers: {
                authorization: "Bearer " + localStorage.getItem("token")
              },
            }
          )
          .then(() => {
            this.message === "";
            this.$router.push("/wall");
          })
          .catch(() => {
            console.log("erreur de modification");
          });
      
    },
  },
};
</script>
<style scoped>

.card {
  max-width: 600px;
  margin: 100px auto;
}


@media screen and (min-width: 320px) and (max-width: 500px) {
  .card {
    margin: 10px;
  }
}


</style>