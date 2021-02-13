<template>
  <div>
    <ligne-filtre v-bind:name="'spellName'"></ligne-filtre>
    <ligne-filtre v-bind:name="'school'"></ligne-filtre>
    <ligne-filtre v-bind:name="'branch'"></ligne-filtre>
    <ligne-filtre v-bind:name="'domain'"></ligne-filtre>
    <ligne-filtre v-bind:name="'level'"></ligne-filtre>
    <ligne-filtre v-bind:name="'available'"></ligne-filtre>
    <ligne-filtre v-bind:name="'add'"></ligne-filtre>
  </div>
</template>

<script>
import LigneFiltre from "@/components/LigneFiltre";
export default {
  name: "FiltreSort",
  components: {LigneFiltre}
}
</script>

<style scoped>

</style>