<template>
    <div class="field">
        <div class="content">
            <h3>Groupomania Users</h3>
            <hr />

            <div class="card" v-for="user in users" :key="user.id">
                <p class="title font-weight-bold">
                    Créé le :{{ user.createdAt }}
                </p>
                <span class="title font-weight-bold"
                    >username : {{ user.username }}</span
                >
                <p class="title font-weight-bold">Email : {{ user.email }}</p>
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
        };
    },
    created() {
        axios
            .get("http://localhost:3000/api/admin/users", {
                headers: { Authorization: "Bearer " + localStorage.token },
            })
            .then((response) => (this.users = response.data.users))
            .catch((err) => console.log(err));
    },
};
</script>
<style scoped>
h3 {
    font-size: 1.9em;
    color: #d1515a;
}
</style>