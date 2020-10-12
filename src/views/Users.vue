<template>
    <div class="container forms">
        <hr />
        <AdminUsers />
    </div>
</template>

<script>
import AdminUsers from "@/components/Forms/AdminUsers.vue";
export default {
    name: "Users",
    components: {
        AdminUsers,
    },
};
</script>

<style scoped>
.forms {
    display: flex;
    justify-content: center;
    margin-top: 160px;
    margin-bottom: 175px;
    font-size: 0.9em;
}
.title {
    color: #122442;
}

.field {
    font-size: 1.8em;
}
</style>