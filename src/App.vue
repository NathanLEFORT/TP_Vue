<template>
  <div>
    <div>
    </div>
    <Configuration/>
    <Recherche/>
    <Stats/>
  </div>
</template>


<script>
import Configuration from "@/components/Configuration";
import Recherche from "@/components/Recherche";
import Stats from "@/components/Stats";
import {sortTable, bookUsed, bookTable} from "../public/data.min.js";

export default {
  name: "App",
  components: {Configuration, Stats, Recherche},
  data () {
    return {
      sortTable: sortTable,
      bookUsed: bookUsed,
      bookTable: bookTable
    }
  }
}

console.log(sortTable[0]);
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
