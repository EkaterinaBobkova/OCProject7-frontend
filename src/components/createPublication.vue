<template>
  <div>
      <h3> Ecrivez quelque chose : </h3>
    <div class="field">
      
      <form enctype="multipart/form-data" action="/create" method="post">
        <div class="control">
         <textarea class="textarea" cols="55" rows="5" v-model="contentPublication.content"  placeholder="Votre message"></textarea>
          <br />
          
        </div>


        <div class="file">
  <label class="file-label">
    <input class="file-input" type="file" name="inputFile"
              id="inputFile"
              aria-describedby="inputFileAddon"
              @change="onFileChange">

    <span class="file-cta">
      <span class="file-icon">
        <i class="fas fa-upload"></i>
      </span>
      <span class="file-label">
        Choisir le fichier
      </span>
    </span>
  </label>
</div>

        <input type="submit" class=" button button is-dark" @click.prevent="createPublication" value="Submit" />
        
      </form>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "CreatePublication",
  data() {
    return {
      contentPublication: {
        content: null,
        postImage: null
      },
      msgError: ""
    };
  },
 
  methods: {
    createPublication() {
      console.log(this.contentPublication);
      const fd = new FormData();
      fd.append("inputFile", this.contentPublication.postImage);
      fd.append("content", this.contentPublication.content);
      console.log("test récup", fd.get("inputFile"));
      console.log("test récup", fd.get("content"));
      if (fd.get("inputFile") == "null" && fd.get("content") == "null") {
        let msgReturn = document.getElementById('msgReturnAPI')
        msgReturn.classList.add('text-danger')
        this.msgError = "Rien à publier";
      } else {
        axios
          .post("http://localhost:3000/api/publications", fd, {
            headers: {
              Authorization: "Bearer " + window.localStorage.getItem("token")
            }
          })
          .then(response => {
           
            if (response) {
              window.location.reload();
            }
          })
          .catch(error => (this.msgError = error));
      }
    },
    onFileChange(e) {
      console.log(e);
      this.contentPublication.postImage = e.target.files[0] || e.dataTransfer.files;
      console.log(this.contentPublication.postImage);
    }
  }
};
</script>

<style>

h3{
    font-weight: bold;
    display: flex;
    justify-content: center;
    color: rgb(189, 16, 16);
}
.field {
    display: flex;
    justify-content: center;
    
}

.button {
    margin-top: 10px;
    
}
</style>
