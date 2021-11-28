<template>
 <div class="history">
     <div  class="title">History</div> <br> <br>
     <div class="display" v-on:click="getData()">{{current || 'No History'}}</div>


 </div>    
</template>

<script>



export default {

   getData() {
   this.$router.poll('/History.vue'); 
      
      this.$router.poll({name:'History.vue', params: {id: '[paramdata]'}});
      console.warn("values : this.equal");
   }
  



}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
