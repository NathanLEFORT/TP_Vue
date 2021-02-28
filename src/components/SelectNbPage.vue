<template>
  <div class="col">
    <select class="form-select" id="resultsSize" v-model="selectedSize" v-on:change="getSpells(1)">
      <option value='10'>10</option>
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
  props: ['size'],
  data() {
    return {
      selectedSize: this.size
    }
  },
  methods: {
    getSpells(page){
      // this.$parent.updateSize(this.selectedSize);
      this.$emit('updateSize', this.selectedSize);
      // this.$parent.getSpells(page);
      this.$emit('getSpells', page);
    }
  }
}
</script>

<style scoped>
</style>