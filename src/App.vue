<template>
  <div>
    <div>
    </div>
    <Configuration v-bind:books="booksPresent"/> <!-- v-bind est utilisé pour passer booksPresent à notre composant, sous le nom books -->
    <Recherche v-bind:utils="sortTable"/>
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
      booksPresent: []
    }
  },
  mounted() { // Seul endroit où est censés executer du JS
    sortTable.forEach(sort => {
      if(!this.booksPresent.includes(sort[0])) this.booksPresent.push(sort[0]); //Stocke les noms de livres dans booksPresent
    });
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
