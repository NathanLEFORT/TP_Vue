<template>
  <div class="col-3">
    <div class="card">
      <div class="card-header">Stats</div>
      <div class="card-body">
        <ul>
          <li>Nombre de sorts : {{nbSorts}}</li>
          <li>Nombre de livres : {{nbLivres}}</li>
          <li>Nombre de sorts moyen : {{nbMoySorts}}</li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Stats",
  props : ['utils'],
  data() {
    return {
      nbSorts : 0,
      nbLivres : 0,
      nbMoySorts : 0
    }
  },
  mounted() {
    this.nbSorts = this.utils.length;
    this.nbLivres = 10;
    this.nbMoySorts = this.nbSorts/this.nbLivres;
  }
}
</script>

<style scoped>

</style>