<template>
  <div class="d-flex align-items-start">
    <div class="nav flex-column nav-pills me-3" id="v-pills-tab" role="tablist" aria-orientation="vertical">
      <button class="nav-link active" id="v-pills-home-tab" data-bs-toggle="pill" data-bs-target="#v-pills-home" type="button" role="tab" aria-controls="v-pills-home" aria-selected="true" v-on:click="enableConfiguration()">Configuration</button>
      <button class="nav-link" id="v-pills-profile-tab" data-bs-toggle="pill" data-bs-target="#v-pills-profile" type="button" role="tab" aria-controls="v-pills-profile" aria-selected="false" v-on:click="enableSearch()">Search</button>
      <button class="nav-link" id="v-pills-messages-tab" data-bs-toggle="pill" data-bs-target="#v-pills-messages" type="button" role="tab" aria-controls="v-pills-messages" aria-selected="false" v-on:click="enableStats()">Stats</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "NavBar",
  methods: {
    enableConfiguration() { // Page display when his variable is true
      this.$parent.isConfiguration = true;
      this.$parent.isSearch = false;
      this.$parent.isStats = false;
    },
    enableSearch() { // Page display when his variable is true
      this.$parent.isConfiguration = false;
      this.$parent.isSearch = true;
      this.$parent.isStats = false;
    },
    enableStats() { // Page display when his variable is true
      this.$parent.isConfiguration = false;
      this.$parent.isSearch = false;
      this.$parent.isStats = true;
    }
  }
}
</script>

<style scoped>

</style>