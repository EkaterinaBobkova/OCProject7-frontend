 <template>
  <div id="wall" class="wall">
    <h1 class="titre title is-size-1">Partager les publications :</h1>
    <Create :submit="onSubmit" />

    <div class="field" id="pubForm">
      <div
        class="card"
        v-for="publication in allPublications"
        :key="publication.id"
      >
        <div class="content">
          <div class="headerPost">
            Publié par <em>{{ publication.User.username }}</em> le
            <em>{{ publication.createdAt.split(" ")[0] }}</em> à
            <em>{{ publication.updatedAt }}</em>
          </div>
          <hr />
          {{ publication.content }}
          <!-- <img  :src="publication.attachment" /> -->
        </div>

        <footer class="card-footer">
          <a href="#" class="card-footer-item"
            ><router-link
              :to="{ name: 'UpdatePost', params: { id: publication.id } }"
              >Modifier</router-link
            ></a
          >
          <a
            href="#"
            @click.prevent="() => deletePost(publication.id)"
            class="card-footer-item"
            >Supprimer</a
          >
        </footer>
        <!-- <button @click="createLike"
                                    > {{publication.likes}}j'aime</button> -->
        <div class="content">
          <div class="heart">
            <i
              class="far fa-heart fa-lg"
              :class="{ fass: hasBeenLiked }"
              @click="like"
            >
            </i>
          </div>
          <p class="likes">{{ likes }} j'aime</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import { mapState } from "vuex";
import Create from "@/components/Forms/Publication/Create.vue";

export default {
  name: "Wall",
  components: {
    Create,
  },
  data() {
    return {
      // count: 0,
      publication: {
        User: "",
        id: "",
        content: "",
        attachment: "",
      },
      allPublications: [],
      likes: 0,
      hasBeenLiked: false,
      props: {
        default: true,
        publication: (route) => ({ search: route.query.q }),
      },
    };
  },
  computed: {
    ...mapState(["user"]),
  },

  methods: {
    setInfos(payload) {
      this.publication = payload.publication;
    },
    loadPosts() {
      axios
        .get("http://localhost:3000/api/publications", {
          headers: {
            Authorization: "Bearer " + localStorage.getItem("token"),
          },
        })
        .then((response) => {
          console.log("publication", response.data);
          this.allPublications = response.data;
        })
        .catch((error) => {
          console.log(error);
        });
    },
    onSubmit() {
      this.loadPosts();
    },
    deletePost(id) {
      const post_id = this.allPublications.findIndex(
        (publication) => publication.id === id
      );
      if (post_id !== -1) {
        this.allPublications.splice(post_id, 1);
        axios
          .delete("http://localhost:3000/api/publications/" + id, {
            headers: {
              Authorization: "Bearer " + localStorage.getItem("token"),
            },
            // data: {
            //   contentPublicationId: this. contentPublication.id,
            // }
          })
          .catch((error) => console.log(error));
      }
    },
    like() {
      console.log(this.$route);
      this.hasBeenLiked ? this.likes-- : this.likes++;
      this.hasBeenLiked = !this.hasBeenLiked;
      const id = this.$route.params.id;
      axios
        .post(
          "http://localhost:3000/api/publications/" + id,
          {
            likes: this.publication.likes,
            postId: this.publication.id,
          },
          {
            headers: {
              authorization: "Bearer " + localStorage.getItem("token"),
            },
          }
        )
        .then(() => {
          this.message === "";
        })
        .catch(() => {
          console.log("erreur ");
        });
    },

    //  createLike() {
    //   if (this.publication.like) {
    //     this.count+=1;
    //     const fd = new FormData();
    //     fd.append("likes", this.publication.likes);

    //     axios
    //       .post("http://localhost:3000/api/publications", fd, {
    //         headers: {
    //           Authorization: "Bearer " + window.localStorage.getItem("token"),
    //         },
    //       })
    //       .then(() => this.submit())
    //       .catch((error) => (this.msgError = error));
    //     this.contentPublications.unshift({

    //       likes: this.publication.likes,

    //     });
    //     this.publication.likes = "";

    //   }
    // },
  },

  mounted() {
    this.loadPosts();
  },
};
</script>

<style lang="scss">
.titre {
  color: #122442;
}
.wall {
  background-color: white;
  min-height: 100%;
  padding: 6rem 0 3rem 0;
}
h1 {
  display: flex;
  justify-content: center;
}

.fass {
  color: #d1515a;
}

.headerPost {
  color: #d1515a;
  font-size: 0.9em;
}
</style>