<template>
  <div>
    <h3>Ecrivez quelque chose :</h3>
    <div class="field">
      <form @submit.prevent="createPublication">
        <div class="control">
          <textarea
            class="textarea"
            cols="55"
            rows="5"
            v-model="contentPublication.content"
            placeholder="Votre message"
          ></textarea>
          <br />
        </div>

        <div class="file">
          <label class="file-label">
            <input
              class="file-input"
              type="file"
              name="inputFile"
              id="inputFile"
              aria-describedby="inputFileAddon"
              @change="onFileChange"
            />

            <span class="file-cta">
              <span class="file-icon">
                <i class="fas fa-upload"></i>
              </span>
              <span class="file-label">Choisir le fichier</span>
            </span>
          </label>
        </div>

        <input type="submit" class="button button is-dark" value="Envoyer" />
      </form>
    </div>
    <div class="field" id="pubForm">
      <div
        class="card"
        v-for="contentPublication in contentPublications"
        :key="contentPublication.id"
      >
        <div class="content">{{ contentPublication.content }} <br> {{ contentPublication.attachment }}</div>

        <footer class="card-footer">
          <a href="#" class="card-footer-item">Modifier</a>
          <a
            href="#"
       
            class="card-footer-item"
          >Supprimer</a>
        </footer>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "CreatePublication",
  props: {
    submit: Function,
  },

  data() {
    return {
      wallCount: 0,
      contentPublications: [],
      contentPublication: {
        content: "",
        attachment: "",
      },
      msgError: "",
    };
  },

  methods: {
    createPublication() {
      if (this.contentPublication.content) {
        this.wallCount++;
        const fd = new FormData();
        fd.append("attachment", this.contentPublication.attachment);
        fd.append("content", this.contentPublication.content);

        axios
          .post("http://localhost:3000/api/publications", fd, {
            headers: {
              Authorization: "Bearer " + window.localStorage.getItem("token"),
            },
          }).then(() => this.submit())

          .catch((error) => (this.msgError = error));
        this.contentPublications.unshift({
          id: this.wallCount,
          content: this.contentPublication.content,
          attachment: this.contentPublication.attachment,
        });

        this.contentPublication.content = "";
        this.contentPublication.attachment = "";
      }
    },
    // deleteWallPost(id) {
    //   const post_id = this.contentPublications.findIndex(
    //     (post) => post.id === id
    //   );

    //   if (post_id !== -1) {
    //     this.contentPublications.splice(post_id, 1);
    //   }
    //   axios
    //     .delete("http://localhost:3000/api/publications/" + id, {
    //       headers: {
    //         Authorization: "Bearer " + localStorage.getItem("token"),
    //       },
    //       // data: {
    //       //   contentPublicationId: this. contentPublication.id,

    //       // }
    //     })

    //     .catch((error) => console.log(error));
    // },
    onFileChange(e) {
      console.log(e);
      this.contentPublication.attachment =
        e.target.files[0] || e.dataTransfer.files;
      console.log(this.contentPublication.attachment);
    },
  },
};
</script>

<style>
h3 {
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

.card {
  display: flex;
  flex-direction: column;
  justify-content: center;
  width: 500px;
  margin-top: 50px;
}

#pubForm {
  display: flex;
  flex-direction: column;
  align-items: center;
}
</style>
