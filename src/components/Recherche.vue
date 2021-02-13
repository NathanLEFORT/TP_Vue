<template>
  <div>
    <h1>Recherche</h1>
    <Table v-bind:sorts = "utils"/>
  </div>
</template>

<script>
import Table from "@/components/Table";
export default {
  name: "Recherche",
  props : ['utils'],
  components : {Table}
}
</script>

<style scoped>

</style>