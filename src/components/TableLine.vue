<template>
  <tr v-on:click="open()">
    <td v-for="index in (1,11)" :key="index">
      <div v-if="Array.isArray(sort[index][0])">
        <p v-for="cont in sort[index]" :key="cont">{{cont.join(' ')}}</p>
      </div>
      <p v-else>{{sort[index].toString()}}</p>
    </td> <!--  -->
  </tr>
</template>

<script>
export default {
  name: "TableLine",
  props : ['sort']
}
</script>

<style scoped>

</style>