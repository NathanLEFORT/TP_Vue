<template>
  <div class="row">
    <div class="col-9">
      <div class="input-group input-group-sm mb-3">
        <span class="input-group-text" id="inputGroup-sizing-sm"> {{ this.name }} </span>
        <select class="form-select form-select-lg" v-model="filter" v-on:change="modifyFilter(index, values)">
          <option selected value="" hidden disabled></option>
          <option v-for="item in this.values" :key="item"> {{ item }}</option>
        </select>
      </div>
    </div>
    <div class="col-3">
      <button class="btn btn-secondary" v-on:click="resetFilter()">reset</button>
    </div>
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
      this.modifyFilter();
    },
    modifyFilter() {
      this.$emit('modifyFilter', this.index, this.filter);
    }
  }
}
</script>

<style scoped>
</style>