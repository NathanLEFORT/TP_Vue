<template>
  <div>
    <h1>Recherche</h1>
    <div>
      <select id="resultsSize" v-model="size" v-on:change="getSpells(1)">
        <option value='50'>50</option>
        <option value='100'>100</option>
        <option value='500'>500</option>
        <option value='1000'>1000</option>
      </select>
      <p v-for="page in (1, nbPages)" :key="page"><a v-on:click="getSpells(page)" >{{page}}.</a></p>
    </div>
    <Table v-bind:sorts="utils"/>
  </div>
</template>

<script>
import Table from "@/components/Table";
export default {
  name: "Recherche",
  props : ['utils','nbPages'],
  components : {Table},
  data(){
    return{
      size : '50'
    }
  },

  mounted() {
    document.querySelector('#resultsSize').value = this.size;
    console.log(this.nbPages);
  },
  methods : {
    getSpells(page=0){
      console.log(page);
      this.$parent.getSpells(this.size, (page-1)*this.size);
    }
  },
  watch: {
    size: (newVal, oldVal) => { // watch it
      console.log('Result changed: ', newVal, ' | was: ', oldVal);
    }
  }
}
</script>

<style scoped>
p{
  display:inline;
  margin: 5px;
}
a {
  color:blue;
}
</style>