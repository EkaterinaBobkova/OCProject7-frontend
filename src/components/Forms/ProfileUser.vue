<template>
    <div class="field">
        <div class="content">
            <h1>Bienvenue {{ user.username }} !</h1>
            <hr />
            <a class="button is-light" v-if="user.isAdmin == true">
                <RouterLink to="/users">Tous les utilisateurs</RouterLink>
            </a>
            <hr />
            <a class="button is-light" v-if="user.isAdmin == true">
                <RouterLink to="/publicationsAdmin"
                    >Toutes les publications utilisateurs</RouterLink
                >
            </a>
            <hr />

            <div class="user">
                <h3>Informations sur votre compte :</h3>

                <span>Username : {{ user.username }}</span>

                <p>Email : {{ user.email }}</p>
                <p>Compte créé le : {{ user.createdAt }}</p>
                <input
                    type="submit"
                    class="btnD"
                    @click="deleteUser(user)"
                    value="Supprimer"
                />
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
        deleteUser(user) {
            axios
                .delete("http://localhost:3000/api/auth/users/" + user.id, {
                    headers: { Authorization: "Bearer " + localStorage.token },
                })
                .then((response) => console.log(response))
                .catch((err) => console.log(err));
            localStorage.clear();
            this.$router.push("/signup");
        },
    },
};
</script>
<style scoped>
.field {
    display: flex;
    justify-content: center;
}
h3 {
    font-size: 1em;
    color: #d1515a;
}
.user {
    font-size: 1.1em;
    color: #122442;
    font-weight: bold;
}
.btnD {
    background-color: #122442;
    color: #ffff;
    margin-top: 10px;
    width: 120px;
    height: 50px;
    font-size: 1.1em;
}
</style>