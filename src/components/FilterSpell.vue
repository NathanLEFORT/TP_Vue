<template>
  <div>
    <TextLineFilter v-bind:name="'name'"></TextLineFilter>
    <TextLineFilter v-bind:name="'level'"></TextLineFilter>
    <SelectLineFilter v-bind:name="'class'" v-bind:values="spellsClasses"></SelectLineFilter>
    <SelectLineFilter v-bind:name="'school'" v-bind:values="spellsSchools"></SelectLineFilter>
    <SelectLineFilter v-bind:name="'branch'" v-bind:values="spellsBranches"></SelectLineFilter>
  </div>
</template>

<script>
import SelectLineFilter from "@/components/SelectLineFilter";
import TextLineFilter from "@/components/TextLineFilter";
export default {
  name: "FilterSpell",
  components: {SelectLineFilter, TextLineFilter},
  props: ['spellsClasses', 'spellsSchools', 'spellsBranches'],
}
</script>

<style scoped>

</style>