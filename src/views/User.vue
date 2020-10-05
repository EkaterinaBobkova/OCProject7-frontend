<template>
 
    <div class="container forms">
   
        <h1 class="title is-size-1">
          <i class="fas fa-cog"></i>Paramètres de votre compte
        </h1>
        <hr />
       <DeleteUser />
    </div>
    

</template>

<script>

import DeleteUser from '@/components/Forms/DeleteUser.vue'
export default {
  name: "User",
  components: {
    
    DeleteUser,
  },

};
</script>

<style scoped>
.forms {
  margin-top: 160px;
  margin-bottom: 175px;
}
.title{
  color: #122442;
}

</style>