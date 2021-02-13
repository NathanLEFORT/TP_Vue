<template>
  <div id="textFilter">
    <label id="text"> {{ this.name }}</label>
    <label>
      <input v-model="this.filter">
    </label>
  </div>

</template>

<script>
export default {
name: "TextLineFilter",
  props: ['name'],
  data() {
  return {
      filter: null
    }
  }
}
</script>

<style scoped>
#textFilter {
  margin: 20px;
}
#text {
  margin-right: 10px;
}
</style>