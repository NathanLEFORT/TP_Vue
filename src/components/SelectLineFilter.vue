<template>
  <div id="selectFilter">
    <label id="select"> {{ this.name }}</label>
    <label>
      <select v-model="filter" v-on:change="modifyFilter(index, values)">
          <option selected value="" hidden disabled></option>
          <option v-for="item in this.values" :key="item"> {{ item }}</option>
      </select>
    </label>
    <button v-on:click="resetFilter()">reset</button>
    <label>{{ this.filter }}</label>
  </div>
</template>

<script>
export default {
  name: "SelectLineFilter",
  props: ['name', 'values', 'index'],
  data() {
    return {
      filter: null
    }
  },
  methods: {
    resetFilter() {
      this.filter = null;
    },
    modifyFilter() {
      this.$parent.modifyFilter(this.index, this.filter);
    }
  }
}
</script>

<style scoped>
#selectFilter {
  margin: 20px;
}
#select {
  margin-right: 10px;
}
</style>