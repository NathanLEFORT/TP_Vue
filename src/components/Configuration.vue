<template>
  <div>
    <h1>Configuration</h1>
    <ul>
      <!-- key est nécessaire avec un v-for, pas donné dans son cours -->
      <SelectLivre v-for="book in books" :key="book" v-bind:book = "book"></SelectLivre> <!-- Test d'affichage des noms de livres récupérés depuis App.vue -->
    </ul>
  </div>
</template>

<script>
import SelectLivre from "@/components/SelectLivre";

export default {
  name: "Configuration",
  components: {SelectLivre},
  props:['books'], //Sert à récupérer books (booksPresent) donnés par App.vue

  // mounted() {
  //   this.books.forEach(book => {
  //     if(sessionStorage.getItem(book) !== '0') {
  //       sessionStorage.setItem(book, '1');
  //     } else {
  //       sessionStorage.setItem(book, '0');
  //     }
  //   });
  // }
}

</script>

<style scoped>

</style>