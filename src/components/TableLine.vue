<template>
  <tr v-on:click="open()">
    <td v-for="index in 5" :key="index">
      <div v-if="Array.isArray(sort[index][0])">
        <p v-for="cont in sort[index]" :key="sort[index].indexOf(cont)">{{cont.join(' ')}}</p>
      </div>
      <p v-else>{{sort[index].toString()}}</p>
    </td> <!--  -->
    <td>
      Click to show more details
    </td>
  </tr>
</template>

<script>
export default {
  name: "TableLine",
  props : ['sort'],
  methods : {
    open(){
      this.$parent.showSpell(this.sort);
    }
  }
}
</script>

<style scoped>

</style>