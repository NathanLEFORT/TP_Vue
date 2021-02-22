<template>
  <div>
    <div class="row">
      <TextLineFilter v-bind:name="'Name'" v-bind:index="0"></TextLineFilter>
    </div>
    <div class="row">
      <TextLineFilter v-bind:name="'Level'" v-bind:index="1"></TextLineFilter>
    </div>
    <div class="row">
      <SelectLineFilter v-bind:name="'Class'" v-bind:values="spellsClasses" v-bind:index="2"></SelectLineFilter>
    </div>
    <div class="row">
      <SelectLineFilter v-bind:name="'School'" v-bind:values="spellsSchools" v-bind:index="3"></SelectLineFilter>
    </div>
    <div class="row">
      <SelectLineFilter v-bind:name="'Branch'" v-bind:values="spellsBranches" v-bind:index="4"></SelectLineFilter>
    </div>
  </div>
</template>

<script>
import SelectLineFilter from "@/components/SelectLineFilter";
import TextLineFilter from "@/components/TextLineFilter";
export default {
  name: "FilterSpell",
  components: {SelectLineFilter, TextLineFilter},
  props: ['spellsClasses', 'spellsSchools', 'spellsBranches'],
  data() {
    return {
      filters: [null, null, null, null, null]
    }
  },
  methods: {
    modifyFilter(index, value) {
      this.filters[index] = value;
    }
  }
}
</script>

<style scoped>

</style>