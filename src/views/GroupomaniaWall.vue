 <template>
  <div id="wall" class="wall">
    <h1 class="title is-size-1">Partager les publications :</h1>
    <CreatePublication :submit="onSubmit" />
    

   <div class="field" id="pubForm">
      <div
        class="card" v-for="publication in allPublications" :key="publication.id"
      >
        <div class="content" >
      {{publication.content}}</div>

      <footer class="card-footer">
          <a href="#" class="card-footer-item">Modifier</a>
          <a
            href="#"
            @click.prevent="() => delete(publication.id)"
            class="card-footer-item"
          >Supprimer</a>
        </footer>
      </div>
    </div>







      <!-- <button @click="() => delete(publication.id)">supprimer</button> -->
    

   
  </div>
</template>

<script>
import axios from "axios";
import CreatePublication from "@/components/createPublication.vue";

export default {
  name: "Wall",
  components: {
    CreatePublication,
  },
  data() {
    return {
      publication: {
        id: "",
        content: "",
        image: "",
      },

      allPublications: [],
    };
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
    onSubmit(){
      this.loadPosts();
    },
    delete(id){
      const post_id = this.contentPublications.findIndex(
        (publication) => publication.id === id
      );

      if (post_id !== -1) {
        this.contentPublications.splice(post_id, 1);
      }
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
    },

    },
  
  mounted() {
    this.loadPosts()
  },
};
</script>

<style lang="scss">
.wall {
  background-color: white;
  min-height: 100%;
  padding: 6rem 0 3rem 0;
}

h1 {
  display: flex;
  justify-content: center;
}
</style>