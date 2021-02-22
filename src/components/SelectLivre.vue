<template>
  <li class="list-group-item">
    <div class="row">
      <div class="col-1">
        <!--  la ckeckbox de sélection du livre -->
        <input class="form-check-input" v-model="isSelect" type="checkbox" v-on:click="setSelect()"/>
      </div>
      <div class="col-11">
        <!-- affichage du nom du livre -->
        {{ this.book }}
      </div>
    </div>
  </li>
</template>

<script>
export default {
  name: "SelectLivre",
  props:['book'],
  data() {
    return {
      isSelect: false
    }
  },
  mounted() {
    this.isSelect = sessionStorage.getItem(this.book) !== null; // initialisation de isSelect  depuis la session
  },
  methods: {
    setSelect() { // mise à jour des données de la session lors de la modification de isSelect
      if(this.isSelect) {
        sessionStorage.removeItem(this.book);
      } else {
        sessionStorage.setItem(this.book, 'true');
      }
    }
  }
}
</script>

<style scoped>

</style>