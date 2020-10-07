<template>
      <img  :src="dataUrl" />
</template>




<script>
export default {
    props: {blob:null},
    data: () => { 
        return {dataUrl:null}
    },
    
    mounted() {
        console.log(this.blob);
        const reader = new FileReader()
        reader.readAsDataURL(new Blob(this.blob,{type:"image/png"}));
        reader.onload = () => {
            console.log(reader.result);
            this.dataUrl = reader.result;

        }

    }
    
}


</script>