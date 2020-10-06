<template>
 
    <div class="container forms">
   
        <h1 class="title is-size-1">
          <i class="fas fa-cog"></i>Paramètres 
        </h1>
        <hr />
       <ProfileUser />
    </div>
    

</template>

<script>

import ProfileUser from '@/components/Forms/ProfileUser.vue'
export default {
  name: "User",
  components: {
    
    ProfileUser,
  },

};
</script>

<style scoped>
.forms {
  margin-top: 160px;
  margin-bottom: 175px;
  font-size: 0.9em;
}
.title{
  color: #122442;
}

</style>