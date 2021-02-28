<template>
    <div class="col-3">
      <div class="card">
        <div class="card-header">Configuration</div>
        <div class="card-body">
          <ul class="list-group">
              <!-- key est nécessaire avec un v-for, pas donné dans son cours -->
              <SelectBook v-for="book in books" :key="book" v-bind:book = "book" @update="updateNbBooks"></SelectBook> <!-- Test d'affichage des noms de livres récupérés depuis App.vue -->
          </ul>
        </div>
      </div>
    </div>
</template>

<script>
import SelectBook from "@/components/SelectBook";

export default {
  name: "Configuration",
  components: {SelectBook},
  props:['books'], //Sert à récupérer books (booksPresent) donnés par App.vue
  methods: {
    updateNbBooks(value) {
      if(value) {
        this.$emit('update', 1);
      } else {
        this.$emit('update', -1);
      }
    }
  }
}

</script>

<style scoped>
</style>