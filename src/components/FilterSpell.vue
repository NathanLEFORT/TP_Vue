<template>
  <div>
    <SelectLineFilter v-bind:name="'class'" v-bind:values="spellsClasses"></SelectLineFilter>
    <SelectLineFilter v-bind:name="'school'" v-bind:values="spellsSchools"></SelectLineFilter>
    <SelectLineFilter v-bind:name="'branch'" v-bind:values="spellsBranches"></SelectLineFilter>
  </div>
</template>

<script>
import SelectLineFilter from "@/components/SelectLineFilter";
export default {
  name: "FilterSpell",
  components: {SelectLineFilter},
  props: ['spellsClasses', 'spellsSchools', 'spellsBranches'],
}
</script>

<style scoped>

</style>