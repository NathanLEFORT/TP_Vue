<template>
  <div class="col-3">
    <div class="card">
      <div class="card-header">Stats</div>
      <div class="card-body">
        <ul>
          <li>Nombre de sorts : {{this.nbBooks}}</li>
          <li>Nombre de livres : {{this.nbSpells}}</li>
          <li>Nombre de sorts moyen :</li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Stats",
  props: ['nbBooks', 'nbSpells']
}
</script>

<style scoped>

</style>