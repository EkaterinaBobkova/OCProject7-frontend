<template>


  <div class="field">
      <form @submit.prevent="editPost">
        <div class="control">
          
          <textarea
            class="textarea"
            id="newText"  
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
  name: "UpdatePost",
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
        editPost() {
       let newMessage = document.getElementById("newText").value;
     
      let newContent = false;
      if (newMessage !== this.editedPost.content != false) {
        newContent = true;
      }
        
      // console.log(this.$router); 
      if (newContent ) {
        axios
          .put(
            "http://localhost:3000/api/publications",
            {
               content: this.editedPost.content,
              postId: this.editedPost.id,
            
           
            },
            {
              headers: {
                authorization: "Bearer " + localStorage.getItem("token")
              }
            }
          )
          .then(() => {
            this.message === "";
            this.$router.push("/wall");
          })
          .catch(() => {
            console.log("erreur de modification");
            
          })}
          else{
        console.log("aucune modification");
      }
    },
  
  }
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
