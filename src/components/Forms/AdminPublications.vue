<template>
    <div class="field">
        <div class="content">
            <h1>Groupomania Users publications</h1>
            <hr />

            <div
                class="card"
                v-for="publication in publications"
                :key="publication.id"
            >
                <span class="title font-weight-bold"
                    >Publié par : {{ publication.User.username }}</span
                >
                <br />

                <span class="title font-weight-bold"
                    >publication : {{ publication.content }}</span
                >
                <br />

                <!-- <BlobImage :blob="publication.attachment.data"/> -->
                <p class="title font-weight-bold">
                    créée le : {{ publication.createdAt }}
                </p>
                <br />
            </div>
        </div>
    </div>
</template>
<script>
import axios from "axios";
export default {
    data() {
        return {
            user: "",
            users: [],
            error: "",
            publications: [],
        };
    },
    created() {
        axios
            .get("http://localhost:3000/api/admin", {
                headers: {
                    Authorization: "Bearer " + localStorage.getItem("token"),
                },
            })
            .then((response) => {
                console.log("publication", response.data);
                this.publications = response.data.publications;
            })
            .catch((error) => {
                console.log(error);
            });
    },
};
</script>
<style scoped>
</style>