<template>
  <div class="container-fluid m-4">
    <div class="row">
      <div class="col-1">
        <NavBar></NavBar>
      </div>
      <div class="col-11">
        <Configuration v-if="this.isConfiguration" v-bind:books="booksPresent"/> <!-- v-bind est utilisé pour passer booksPresent à notre composant, sous le nom books -->
        <Recherche v-else-if="this.isSearch" v-bind:utils="spellsKept" v-bind:nbPages="nbPages" v-bind:spells="sortTable"/>
        <Stats v-else-if="this.isStats" v-bind:utils="sortTable"/>
      </div>
    </div>
  </div>
</template>


<script>
import Configuration from "@/components/Configuration";
import Recherche from "@/components/Recherche";
import Stats from "@/components/Stats";
import {sortTable} from "../public/data.min.js";
import NavBar from "@/components/NavBar";

export default {
  name: "App",
  components: {NavBar, Configuration, Stats, Recherche},
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
  }
}


</script>

<style>
</style>
