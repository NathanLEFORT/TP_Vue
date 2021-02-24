<template>
  <div>
    <table class="table table-striped">
      <TableHead/>
      <tbody>
        <TableLine v-for="sort in sorts" :key="sort[1]" v-bind:sort="sort"/>
      </tbody>
    </table>
  </div>
</template>

<script>
import TableHead from "@/components/TableHead";
import TableLine from "@/components/TableLine";
export default {
name: "Table",
  props : ['sorts'],
  components : {TableLine, TableHead},
  methods : {
    showSpell(spell){
      this.$parent.showSpell(spell);
    }
  }
}
</script>

<style scoped>

</style>