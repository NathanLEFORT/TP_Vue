<template>
  <div>
    <div>
    </div>
    <Configuration v-bind:books="booksPresent"/> <!-- v-bind est utilisé pour passer booksPresent à notre composant, sous le nom books -->
    <Recherche v-bind:utils="spellsKept" v-bind:nbPages="nbPages"/>
    <Stats v-bind:utils="sortTable"/>
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
      nbPages : 0
    }
  },
  mounted() { // Seul endroit où est censés executer du JS
    this.getBooks();
    this.getSpellsFromBooks();
    this.getSpells(50);
  },
  methods : {
    getSpells(size, offset=0){
      this.spellsKept = this.spells.slice(offset,offset+size); //Garde les sorts de la liste à afficher
      this.nbPages=Math.ceil(this.spells.length / size);
      console.log(this.nbPages);
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
    }
  }
}


</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
