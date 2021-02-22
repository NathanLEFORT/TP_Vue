<template>
  <div>
    <div>
      <ul class="nav justify-content-center">
        <li class="nav-item">
          <button class="btn btn-primary" v-on:click="enableConfiguration()">Configuration</button>
        </li>
        <li class="nav-item">
          <button class="btn btn-primary" v-on:click="enableSearch()">Search</button>
        </li>
        <li class="nav-item">
          <button class="btn btn-primary" v-on:click="enableStats()">Stats</button>
        </li>
      </ul>
    </div>
    <Configuration v-if="this.isConfiguration" v-bind:books="booksPresent"/> <!-- v-bind est utilisé pour passer booksPresent à notre composant, sous le nom books -->
    <Recherche v-if="this.isSearch" v-bind:utils="spellsKept" v-bind:nbPages="nbPages" v-bind:spells="sortTable"/>
    <Stats v-if="this.isStats" v-bind:utils="sortTable"/>
  </div>
</template>


<script>
import Configuration from "@/components/Configuration";
import Recherche from "@/components/Recherche";
import Stats from "@/components/Stats";
import {sortTable} from "../public/data.min.js";

export default {
  name: "App",
  components: {Configuration, Stats, Recherche},
  data () {
    return {
      sortTable: sortTable,
      booksPresent: [],
      spells : [],
      spellsKept : [],
      nbPages : 0,
      isConfiguration: true,
      isSearch: false,
      isStats: false
    }
  },
  mounted() { // Seul endroit où est censés executer du JS
    this.getBooks();
    this.getSpellsFromBooks();
    this.getSpells(50,0);
  },
  methods : {
    getSpells(size, offset, filters=null){
      if(filters==null){
        this.spellsKept = this.spells.slice(offset,offset+size); //Garde les sorts de la liste à afficher
      }
      else {
        let name = filters[0];
        let level = filters[1];
        let classes = filters[2];
        let school = filters[3];
        let branch = filters[4];

        this.spellsKept = this.getFiltered(name, level, classes, school, branch).slice(offset, offset+size);
      }
      this.nbPages=Math.ceil(this.spells.length / size);
      console.log(this.nbPages);
    },

    getFiltered(name, level, classes, school, branch){
      let filteredSpells=[];

      this.spells.forEach(spell => {
        let add = true;
        if(classes!=null){
          add = this.verifySpellClassAndLevel(spell[4], classes, level);
        }
        else if (level!=null){
          add = this.verifySpellLevel(spell[4], level);
        }

        if(add && name!=null){
          add = spell[1]===name;
        }

        if(add && school!=null){
          add = spell[2]===name;
        }

        if(add && branch!=null){
          add = spell[3]===branch;
        }

        if(add===true){ // If all criteria are respected we add the spell to the list
          filteredSpells.push(spell);
        }
      });

      return filteredSpells;
    },

    verifySpellClassAndLevel(spellClass, classes, level){
      let spellClasses = [];
      spellClass.forEach(double =>{
        spellClasses.push(double[0]);
      });

      if(spellClass.contains(classes)){
        let ind = spellClass.indexOf(classes);
        return !(level != null && spellClass[ind][1] !== level);
      }
      else {
        return false;
      }
    },

    verifySpellLevel(spellClass, level){
        let spellLevel = false;
        spellClass.forEach(double =>{
          if(double[1]===level) {
            spellLevel = true;
          }
        });
        return spellLevel;
    },

    getSpellsFromBooks(){
      this.sortTable.forEach(spell => {
        if (sessionStorage.getItem(spell[0]) != null) this.spells.push(spell); //Garde les sorts uniquements des livres selectionnés
      });
    },

    getBooks(){
      this.sortTable.forEach(spell => {
        if (!this.booksPresent.includes(spell[0])) this.booksPresent.push(spell[0]); //Garde les sorts uniquements des livres selectionnés
      });
    },

    enableConfiguration() {
      this.isConfiguration = true;
      this.isSearch = false;
      this.isStats = false;
    },
    enableSearch() {
      this.isConfiguration = false;
      this.isSearch = true;
      this.isStats = false;
    },
    enableStats() {
      this.isConfiguration = false;
      this.isSearch = false;
      this.isStats = true;
    }

  }
}


</script>

<style>
</style>
