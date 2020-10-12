<template>
    <div>
        <h3>Ecrivez quelque chose :</h3>
        <br />
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
                            @change="uploadImage"
                        />

                        <span class="file-cta">
                            <span class="file-icon">
                                <i class="fas fa-upload"></i>
                            </span>
                            <span class="file-label" for="inputFile"
                                >Choisir le fichier</span
                            >
                        </span>
                    </label>
                </div>

                <input type="submit" class="btnS" value="Envoyer" />
            </form>
        </div>
        <div class="field" id="pubForm">
            <div
                class="card"
                v-for="contentPublication in contentPublications"
                :key="contentPublication.id"
            >
                <div class="content">
                    <!-- {{ contentPublication.content }} <br />

                    <img class="postImg" :src="contentPublication.attachment" /> -->
                </div>
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
                fd.append("inputFile", this.contentPublication.attachment);
                fd.append("content", this.contentPublication.content);

                axios
                    .post("http://localhost:3000/api/publications", fd, {
                        headers: {
                            Authorization:
                                "Bearer " +
                                window.localStorage.getItem("token"),
                        },
                    })
                    .then(() => this.submit())
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

        uploadImage(evt) {
            const files = evt.target.files;
            if (!files.length) return;
            const reader = new FileReader();
            reader.readAsDataURL(files[0]);
            reader.onload = (evt) => {
                this.contentPublication.attachment = evt.target.result;
            };
            // To enable reuploading of same files in Chrome
            document.querySelector("#inputFile").value = "";
        },
    },
};
</script>

<style>
h3 {
    font-weight: bold;
    display: flex;
    justify-content: center;
    color: #d1515a;
}
.field {
    display: flex;
    justify-content: center;
}
.button {
    margin-top: 10px;
}
.card {
    text-align: justify;
    width: 400px;
    margin-top: 50px;
}
#pubForm {
    display: flex;
    flex-direction: column;
    align-items: center;
}
.content {
    display: flex;
    flex-direction: column;
    margin-right: 30px;
    margin-left: 30px;
    justify-content: center;
    align-items: center;
}
.postImg {
    width: 150px;
}

.btnS {
    background-color: #122442;
    color: #ffff;
    margin-top: 10px;
    width: 100px;
    height: 50px;
    font-size: 1.3em;
}
</style>
