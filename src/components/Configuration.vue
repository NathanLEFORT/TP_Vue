<template>
    <div class="col-3">
      <div class="card">
        <div class="card-header">
          Configuration
        </div>
        <div class="card-body">
          <ul class="list-group">
              <!-- key est nécessaire avec un v-for, pas donné dans son cours -->
              <SelectLivre v-for="book in books" :key="book" v-bind:book = "book"></SelectLivre> <!-- Test d'affichage des noms de livres récupérés depuis App.vue -->
          </ul>
        </div>
      </div>
    </div>
</template>

<script>
import SelectLivre from "@/components/SelectLivre";

export default {
  name: "Configuration",
  components: {SelectLivre},
  props:['books'], //Sert à récupérer books (booksPresent) donnés par App.vue

}

</script>

<style scoped>

</style>