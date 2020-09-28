<template>


  <div class="field">
      <form @submit="(evt) => evt.preventDefault() || editPost(editedPost.id)">
        <div class="control">
          
          <textarea
            class="textarea"
            cols="55"
            rows="5"
           v-model="editedPost.content"
            placeholder="Modifiez votre message"
          ></textarea>
          <br />
        </div>

      

        <input type="submit" class="button button is-dark" value="Envoyer" />
      </form>
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
        
      console.log(this.$router);
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
