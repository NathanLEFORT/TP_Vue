<template>
  <div>
    <FilterSpell v-bind:spellsClasses="spellsClasses" v-bind:spellsSchools="spellsSchools" v-bind:spellsBranches="spellsBranches" @getFilteredSpells="getFilteredSpells"></FilterSpell>
    <div class="row p-2">
      <SelectNbPage v-bind:size="this.size" @updateSize="updateSize" @getSpells="getSpells"></SelectNbPage>
      <div class="col-9">
        <div class="btn-group" role="group">
          <button class="btn btn-primary" v-for="page in (nbPages)" :key="page"><a v-on:click="getSpells(page)" >{{page}}.</a></button>
        </div>
      </div>
    </div>
    <div class = row><div class="col-11">
        <Table v-bind:sorts="utils" v-if="this.isSpellList"></Table>
        <SpellCard v-else v-bind:spell="selectedSpell"></SpellCard>
    </div></div>
  </div>
</template>

<script>
import Table from "@/components/Table";
import FilterSpell from "@/components/FilterSpell";
import SelectNbPage from "@/components/SelectNbPage";
import SpellCard from "@/components/SpellCard";
export default {
  name: "Recherche",
  props : ['utils','nbPages', 'spells'],
  components : {SelectNbPage, FilterSpell, Table, SpellCard},
  data(){
    return{
      size : '50',
      spellsClasses: [],
      spellsSchools: [],
      spellsBranches: [],
      selectedSpell: [],
      isSpellList: true
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
      this.$emit('getSpells', this.size, page);
    },

    getFilteredSpells(filters){
      this.$emit('getSpells', this.size, 1, filters);
    },

    showSpell(spell){
      this.selectedSpell=spell;
      this.isSpellList=false;
    },

    showList(){
      this.isSpellList=true;
    },
    updateSize(size) {
      this.size = size;
    }
  }
}
</script>

<style scoped>
</style>