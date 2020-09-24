<template>
 
    <div class="container">
   
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