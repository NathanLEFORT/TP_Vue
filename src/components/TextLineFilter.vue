<template>
  <div class="row">
    <div class="col-9">
      <div class="input-group input-group-sm mb-3">
        <span class="input-group-text" id="inputGroup-sizing-sm"> {{ this.name }} </span>
        <input type="text" class="form-control" aria-label="Sizing example input" aria-describedby="inputGroup-sizing-sm" v-model="filter" v-on:change="update">
      </div>
    </div>
  </div>
</template>

<script>
export default {
name: "TextLineFilter",
  props: ['name','index'],
  data() {
  return {
      filter: null
    }
  },
  methods : {
    update(){
      this.$emit('modifyFilter', this.index, this.filter);
    }
  }
}
</script>

<style scoped>
</style>