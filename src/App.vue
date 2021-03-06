<template>
  <div class="container-fluid m-4">
    <div class="row">
      <div class="col-1">
        <NavBar></NavBar>
      </div>
      <div class="col-11">
        <Configuration v-if="this.isConfiguration" v-bind:books="booksPresent" @update="UpdateNbBooks"/> <!-- v-bind est utilisé pour passer booksPresent à notre composant, sous le nom books -->
        <Recherche v-else-if="this.isSearch" v-bind:utils="spellsKept" v-bind:nbPages="nbPages" v-bind:spells="sortTable" @getSpells="getSpells"/>
        <Stats v-else-if="this.isStats" :nbBooks="nbBooksSelected" :nbSpells="nbSpellsSelected"/>
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
      spellsFiltered : [],
      spellsKept : [],
      nbPages : 0,
      page : 1,
      isConfiguration: true,
      isSearch: false,
      isStats: false,
      nbSpellsSelected: 0,
      nbBooksSelected: sessionStorage.getItem('nbBooksSelected')
    }
  },
  mounted() {
    this.getBooks();
    this.getSpellsFromBooks();
    this.getSpells(50,1);
  },
  methods : {
    getSpells(size, page, filters=null){
      this.page=page;
      let offset = (page-1)*size;
      if(filters==null){
        this.spellsKept = this.spells.slice(offset,offset+size); //Garde les sorts de la liste à afficher
        this.nbPages=Math.ceil(this.spells.length / size);
      }
      else {
        let name = filters[0];
        let level = filters[1];
        let classes = filters[2];
        let school = filters[3];
        let branch = filters[4];
        this.spellsFiltered=this.getFiltered(name, level, classes, school, branch);
        this.spellsKept = this.spellsFiltered.slice(offset, offset+size);
        this.nbPages=Math.ceil(this.spellsFiltered.length / size);
      }
    },

    getFiltered(name, level, classes, school, branch){
      let filteredSpells=[];

      this.spells.forEach(spell => {
        let add = true;

        if(classes!=null){
          add = this.verifySpellClassAndLevel(spell[4], classes, level);
        }
        else if (level!=null && level!==""){
          add = this.verifySpellLevel(spell[4], level);
        }

        if(add && name!=null && name!==""){
          add = spell[1].includes(name);
        }

        if(add && school!=null){
          add = spell[2]===school;
        }

        if(add && branch!=null){
          add = spell[3]==branch;
        }

        if(add===true){ // If all criteria are respected we add the spell to the list
          filteredSpells.push(spell);
        }
      });

      return filteredSpells;
    },

    // If a class is specified in the filters, compare Class filter to spell class, and spell level for given
    // Class to Level filter (if defined)
    verifySpellClassAndLevel(spellClass, classes, level){
      let found = false;
      spellClass.forEach(double =>{
        if(double[0]===classes){
          found = !(level != null && level !== "" && double[1].toString() !== level.toString());
        }
      });
      return found;
    },

    // If no class is specified in the filters, compare Level filter to all possible Levels of the spell
    verifySpellLevel(spellClass, level){
      let spellLevel = false;
      spellClass.forEach(double =>{
        if(double[1]==level) {
          spellLevel = true;
        }
      });
      return spellLevel;
    },

    // Recover spells only from books selected in Configuration tab
    getSpellsFromBooks(){
      this.spells = [];
      this.sortTable.forEach(spell => {
        if (sessionStorage.getItem(spell[0]) != null) this.spells.push(spell); //Garde les sorts uniquements des livres selectionnés
      });
      this.nbSpellsSelected = this.spells.length;
    },

    getBooks() {
      this.sortTable.forEach(spell => {
        if (!this.booksPresent.includes(spell[0])) this.booksPresent.push(spell[0]); //Garde les sorts uniquements des livres selectionnés
      });
    },

    UpdateNbBooks(value) {
      if(sessionStorage.getItem('nbBooksSelected'))
        this.nbBooksSelected = parseInt(sessionStorage.getItem('nbBooksSelected'));
      this.nbBooksSelected = this.nbBooksSelected + value;
      sessionStorage.setItem('nbBooksSelected', this.nbBooksSelected);
    }
  }
}
</script>

<style>
</style>
