<template>
  <div>
    <FilterSpell v-bind:spellsClasses="spellsClasses" v-bind:spellsSchools="spellsSchools" v-bind:spellsBranches="spellsBranches"></FilterSpell>
    <div class="row p-2">
      <SelectNbPage v-bind:size="this.size"></SelectNbPage>
      <div class="col-9">
        <div class="btn-group" role="group">
          <button class="btn btn-primary" v-for="page in (nbPages)" :key="page"><a v-on:click="getSpells(page)" >{{page}}.</a></button>
        </div>
      </div>
    </div>
    <Table v-bind:sorts="utils"/>
  </div>

</template>

<script>
import Table from "@/components/Table";
import FilterSpell from "@/components/FilterSpell";
import SelectNbPage from "@/components/SelectNbPage";
export default {
  name: "Recherche",
  props : ['utils','nbPages', 'spells'],
  components : {SelectNbPage, FilterSpell, Table},
  data(){
    return{
      size : '50',
      spellsClasses: [],
      spellsSchools: [],
      spellsBranches: []
    }
  },

  mounted() {
    document.querySelector('#resultsSize').value = this.size;
    console.log(this.nbPages);

    this.spells.forEach(spell => {
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
  },
  methods : {
    getSpells(page=0){
      this.$parent.getSpells(this.size, page);
    },

    getFilteredSpells(filters){
      this.$parent.getSpells(this.size, 1, filters);
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