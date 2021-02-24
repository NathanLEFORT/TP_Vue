<template>
  <div>
    <div class="row">
      <div class="col-3">
        <div class="card">
          <div class="card-header">Search</div>
          <div class="card-body">
            <FilterSpell v-bind:spellsClasses="spellsClasses" v-bind:spellsSchools="spellsSchools" v-bind:spellsBranches="spellsBranches"></FilterSpell>
          </div>
        </div>
      </div>
    </div>

    <div class="row">
      <div class="col-3">
        <select class="form-select" id="resultsSize" v-model="size" v-on:change="getSpells(1)">
          <option value='50'>50</option>
          <option value='100'>100</option>
          <option value='500'>500</option>
          <option value='1000'>1000</option>
        </select>
      </div>
      <div class="col-9">
        <div class="btn-group" role="group">
          <button class="btn btn-primary" v-for="page in (1, nbPages)" :key="page"><a v-on:click="getSpells(page)" >{{page}}.</a></button>
        </div>
      </div>
      <Table v-bind:sorts="utils"/>
    </div>
  </div>
</template>

<script>
import Table from "@/components/Table";
import FilterSpell from "@/components/FilterSpell";
export default {
  name: "Recherche",
  props : ['utils','nbPages', 'spells'],
  components : {FilterSpell, Table},
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
  }
}
</script>

<style scoped>
</style>