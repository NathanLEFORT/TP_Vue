<template>
  <div>
    <table>
      <TableLine v-bind:sort="sort"/>
    </table>
  </div>
</template>

<script>
import TableLine from "@/components/TableLine";
export default {
name: "Table",
  props : ['sorts'],
  components : {TableLine},
  data() {
    return{
      sort: []
    }
  },
  mounted() {
    this.sort=this.sorts[0];
  }
}
</script>

<style scoped>

</style>