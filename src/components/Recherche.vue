<template>
  <div>
    <h1>Recherche</h1>
    <select v-model="getSpells" id="resultsSize">
      <option value="50">50</option>
      <option value="1O0">100</option>
      <option value="500">500</option>
      <option value="1000">1000</option>
    </select>
    <Table v-bind:sorts="spells"/>
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
      spells : [],
      size : 50,
      s : []
    }
  },
  mounted() {
    this.getSpells();
    this.s.forEach(spell => {
      if (sessionStorage.getItem(spell[0]) != null) this.spells.push(spell);
    });
  },
  methods: {
    getSpells(){
      let newSize = document.querySelector('#resultsSize').value;
      if(this.size != newSize) {
        this.size = newSize;
        this.s = this.$parent.getSpells(this.size);
      }
    }
  }
}
</script>

<style scoped>

</style>