<template>
  <tr>
    <td>{{sort[0]}}</td>
    <td>{{sort[1]}}</td>
    <td>{{sort[2]}}</td>
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