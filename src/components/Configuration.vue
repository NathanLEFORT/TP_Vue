<template>
  <div>
    <h1>Configuration</h1>
    <ul>
      <!-- key est nécessaire avec un v-for, pas donné dans son cours -->
      <li v-for="book in books" :key="book">{{book}}</li> <!-- Test d'affichage des noms de livres récupérés depuis App.vue -->
    </ul>
  </div>
</template>

<script>
export default {
  name: "Configuration",
  props:['books'] //Sert à récupérer books (booksPresent) donnés par App.vue
}


</script>

<style scoped>

</style>