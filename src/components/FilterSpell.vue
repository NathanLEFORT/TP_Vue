<template>
  <div>
    <LineFilter></LineFilter>
  </div>
</template>

<script>
import LineFilter from "@/components/LineFilter";
export default {
  name: "FilterSpell",
  components: {LineFilter},
  props: ['spellsClasses', 'spellsSchools', 'spellsBranches']
}
</script>

<style scoped>

</style>