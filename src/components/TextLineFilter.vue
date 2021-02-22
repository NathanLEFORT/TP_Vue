<template>
  <div id="textFilter">
    <label id="text"> {{ this.name }}</label>
    <label>
      <input v-model="filter" v-on:change="update">
    </label>
  </div>

</template>

<script>
export default {
name: "TextLineFilter",
  props: ['name', 'index'],
  data() {
    return {
      filter : ""
    }
  },
  methods : {
    update(){
      this.$parent.modifyFilter(this.index, this.filter);
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