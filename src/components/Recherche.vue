<template>
  <div>
    <h1>Recherche</h1>
    <select id="resultsSize" v-model="size" v-on:change="getSpells()">
      <option value='50'>50</option>
      <option value='100'>100</option>
      <option value='500'>500</option>
      <option value='1000'>1000</option>
    </select>
    <Table v-bind:sorts="utils"/>
  </div>
</template>

<script>
import Table from "@/components/Table";
export default {
  name: "Recherche",
  props : ['utils'],
  components : {Table},
  data(){
    return{
      size : '50'
    }
  },

  mounted() {
    document.querySelector('#resultsSize').value = this.size;
  },
  methods : {
    getSpells(){
      console.log(this.size);
      this.$parent.getSpells(this.size);
      console.log(this.utils);
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

</style>