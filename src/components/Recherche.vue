<template>
  <div>
    <h1>Recherche</h1>

    <FiltreSort v-bind:spellsClasses="spellsClasses" v-bind:spellsSchools="spellsSchools" v-bind:spellsBranches="spellsBranches"></FiltreSort>

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
import FiltreSort from "@/components/FilterSpell";
export default {
  name: "Recherche",
  props : ['utils'],
  components : {Table, FiltreSort},
  data(){
    return{
      spells : [],
      size : 50,
      s : [],
      spellsClasses: [],
      spellsSchools: [],
      spellsBranches: []
    }
  },
  mounted() {
    this.utils.forEach(spell => {
      if (sessionStorage.getItem(spell[0]) != null) this.spells.push(spell);
    });

    this.utils.forEach(spell => {
      if(this.spellsClasses.indexOf(spell[4][0][0]) === -1) {
        this.spellsClasses.push(spell[4][0][0]);
      }
      if(this.spellsSchools.indexOf(spell[2]) === -1) {
        this.spellsSchools.push(spell[2]);
      }
      spell[3].forEach(branch => {
        if(this.spellsBranches.indexOf(branch) === -1){
          this.spellsBranches.push(branch);
        }
      });
    })
    console.log(this.spellsLevels)
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