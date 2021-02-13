<template>
  <div>
    <a>{{ this.name }}</a>
    <label>
      <select>
        <option></option>
      </select>
    </label>
  </div>
</template>

<script>
export default {
  name: "LigneFiltre",
  props: ['name']
}
</script>

<style scoped>

</style>