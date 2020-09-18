 <template>
   
        
  <div id="wall" class="wall">
      
 <h1 class="title is-size-1">Partager les publications : </h1> 
        <CreatePublication />


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
        image: ""
      },
     
      allPublications: []
   
    };
  },
 
 methods: {
    setInfos(payload) {
      this.publication = payload.publication;
    }
  },
  mounted() {
    axios
      .get("http://localhost:3000/api/publications", {
        headers: {
          Authorization: "Bearer " + localStorage.getItem("token")
        }
      })
     
      .then(response => {
        console.log("publication", response.data);
        this.allPublications = response.data;
      })
      .catch(error => {
        console.log(error); 
      }),
      
      this.$store.dispatch("getUserInfos");
  }
};
</script>

<style lang="scss">
.wall {
  background-color: white;
  min-height: 100%;
  padding: 6rem 0 3rem 0;
}

h1{
    display: flex;
    justify-content: center;
   
}
</style>