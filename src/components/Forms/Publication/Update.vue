<template>
  <div >
    <div >
      <!--Modification -->
      <div v-if="editOption=='modify'">
        <div >
          <h5 id="ModalLabel">Modifier le post</h5>
          <button type="button" class="close" data-dismiss="modal" aria-label="Close">
            <span aria-hidden="true">&times;</span>
          </button>
        </div>
        <div >
          <form enctype="multipart/form-data" action="/update" method="put">
            <div >
              <label for="input_text">Modifiez votre message</label>
              <br />
              <textarea id="inputNewText" type="text" :value="publication.content"></textarea>
            </div>
            <div  v-if="publication.attachement">
              <br />
              <img  :src="publication.attachement" />
              <button type="button"  @click='deleteImgAction'>Delete image</button>
            </div>

            <span id="msgReturnAPI" ></span>
          </form>
        </div>
        <div >
          <button type="button" data-dismiss="modal">Annuler</button>
          <button type="button"  @click="updatePost">Save changes</button>
        </div>
      </div>

      <!--Une suppression -->
      <div  v-else>
        <div >
          <h5 id="ModalLabel">Supprimer ce post (id: {{publication.id}})</h5>
          <button type="button" class="close" data-dismiss="modal" aria-label="Close">
            <span aria-hidden="true">&times;</span>
          </button>
        </div>
        <div >
          <p>Etes vous sûr de vouloir supprimer ce post</p>
        </div>
        <div >
          <button type="button"  data-dismiss="modal">Annuler</button>
          <button type="button" @click="deletePost">Delete post</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { mapState } from "vuex";
import axios from "axios";
export default {
  name: "modalBoxModerate",
  data() {
    return {
      deleteImg: false
    };
  },
  computed: {
    ...mapState(["user", "editOption"])
  },
  props: {
    publication: {
      type: Object,
      default() {}
    }
  },
  methods: {

    updatePost() {
      let newInput = document.getElementById("inputNewText").value;
      //Verification si changements existent
      let newContent = false;
      if (newInput !== this.publication.content || this.deleteImg != false) {
        newContent = true;
      }
      //Modificiation si changements existent
      if (newContent && this.deleteImg) {
        axios
          .put(
            "http://localhost:3000/api/publications",
            {
              postId: this.publication.id,
              userIdOrder: this.user.userId,
              newText: newInput,
              newImg: null
            },
            {
              headers: {
                authorization: "Bearer " + localStorage.getItem("token")
              }
            }
          )
          .then(response => {
            console.log("reponse API", response);
            this.retourAPI = response.data.confirmation;
            setTimeout(() => {
              this.retourAPI = "";
              // window.location.reload();
            }, 2000);
          })
          .catch(err => {
            console.log("admin", err);
            this.retourAPI = "Une erreur est survenue, vérifier vos saisies";
          })
      } else if(newContent){
        axios
          .put(
            "http://localhost:3000/api/publications",
            {
              postId: this.publication.id,
              userIdOrder: this.user.userId,
              newText: newInput,
            },
            {
              headers: {
                authorization: "Bearer " + localStorage.getItem("token")
              }
            }
          )
          .then(response => {
            console.log("reponse API", response);
            this.retourAPI = response.data.confirmation;
            setTimeout(() => {
              this.retourAPI = "";
              // window.location.reload();
            }, 2000);
          })
          .catch(err => {
            console.log("admin", err);
            this.retourAPI = "Une erreur est survenue, vérifier vos saisies";
          })}
          else{
        console.log("aucun changement");
      }
    },
    deleteImgAction() {
      this.deleteImg = true;
    }
  }
};
</script>

<style>
</style>