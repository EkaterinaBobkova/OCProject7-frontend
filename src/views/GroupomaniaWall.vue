  <template>
    <div id="wall" class="wall">
        <h1 class="titre title">Partager les publications :</h1>

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
                    <BlobImage :blob="publication.attachment.data" />
                </div>

                <footer class="card-footer">
                    <a
                        href="#"
                        class="card-footer-item"
                        v-if="
                            publication.UserId == user.id ||
                            user.isAdmin == true
                        "
                        ><router-link
                            :to="{
                                name: 'UpdatePost',
                                params: { id: publication.id },
                            }"
                            >Modifier</router-link
                        ></a
                    >
                    <a
                        href="#"
                        class="card-footer-item"
                        v-if="
                            publication.UserId == user.id ||
                            user.isAdmin == true
                        "
                        @click.prevent="() => deletePost(publication.id)"
                        >Supprimer</a
                    >
                </footer>
            </div>
        </div>
    </div>
</template>

<script>
import axios from "axios";

import Create from "@/components/Forms/Publication/Create.vue";
import BlobImage from "@/components/Forms/Publication/BlobImage.vue";
export default {
    name: "Wall",
    components: {
        Create,
        BlobImage,
    },
    data() {
        return {
            user: "",
            publication: {
                User: "",
                id: "",
                content: "",
                attachment: "",
                UserId: "",
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
    created() {
        axios
            .get("http://localhost:3000/api/auth", {
                headers: { Authorization: "Bearer " + localStorage.token },
            })
            .then((response) => (this.user = response.data.user))
            .catch((err) => console.log(err));
    },
    methods: {
        setInfos(payload) {
            this.publication = payload.publication;
        },
        loadPosts() {
            axios
                .get("http://localhost:3000/api/publications", {
                    headers: {
                        Authorization:
                            "Bearer " + localStorage.getItem("token"),
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
                            Authorization:
                                "Bearer " + localStorage.getItem("token"),
                        },
                    })
                    .catch((error) => console.log(error));
            }
        },
    },
    mounted() {
        this.loadPosts();
    },
};
</script>

<style lang="scss">
.titre {
    color: #122442;
    font-size: 2em;
    @media screen and (max-width: 1000px) {
        font-size: 1em;
    }
}
.wall {
    background-color: rgb(240, 233, 233);
    min-height: 100%;
    padding: 6rem 0 3rem 0;
    @media screen and (max-width: 1000px) {
        margin-top: 50px;
    }
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