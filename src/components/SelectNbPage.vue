<template>
  <div class="col">
    <select class="form-select" id="resultsSize" v-model="size" v-on:change="$parent.getSpells(1)">
      <option value='50'>50</option>
      <option value='100'>100</option>
      <option value='500'>500</option>
      <option value='1000'>1000</option>
    </select>
  </div>
</template>

<script>
export default {
name: "SelectNbPage",
  props: ['size']
}
</script>

<style scoped>

</style>