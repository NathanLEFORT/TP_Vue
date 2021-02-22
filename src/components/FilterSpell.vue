<template>
  <div>
    <TextLineFilter v-bind:name="'name'" v-bind:index="0"></TextLineFilter>
    <TextLineFilter v-bind:name="'level'" v-bind:index="1"></TextLineFilter>
    <SelectLineFilter v-bind:name="'class'" v-bind:values="spellsClasses" v-bind:index="2"></SelectLineFilter>
    <SelectLineFilter v-bind:name="'school'" v-bind:values="spellsSchools" v-bind:index="3"></SelectLineFilter>
    <SelectLineFilter v-bind:name="'branch'" v-bind:values="spellsBranches" v-bind:index="4"></SelectLineFilter>
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