<template>
  <div class="row">
    <div class="col-3">
      <div class="card">
        <div class="card-header">Search</div>
        <div class="card-body">
          <div class="row"><TextLineFilter v-bind:name="'Name'" v-bind:index="0" @modifyFilter="modifyFilter"></TextLineFilter></div>
          <div class="row"><TextLineFilter v-bind:name="'Level'" v-bind:index="1" @modifyFilter="modifyFilter"></TextLineFilter></div>
          <div class="row"><SelectLineFilter v-bind:name="'Class'" v-bind:values="spellsClasses" v-bind:index="2" @modifyFilter="modifyFilter"></SelectLineFilter></div>
          <div class="row"><SelectLineFilter v-bind:name="'School'" v-bind:values="spellsSchools" v-bind:index="3" @modifyFilter="modifyFilter"></SelectLineFilter></div>
          <div class="row"><SelectLineFilter v-bind:name="'Branch'" v-bind:values="spellsBranches" v-bind:index="4" @modifyFilter="modifyFilter"></SelectLineFilter></div>
        </div>
      </div>
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
      //filters contains the five current filters [Name, Level, Class, School, Branch]
      filters: [null, null, null, null, null]
    }
  },
  methods: {
    modifyFilter(index, value) {
      // When a filter change we update the result table
      this.filters[index] = value;
      this.$emit('getFilteredSpells', this.filters);
    }
  }
}
</script>

<style scoped>

</style>