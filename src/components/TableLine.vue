<template>
  <tr>
    <td v-for="index in (1,11)" :key="index">{{sort[index]}}</td>
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