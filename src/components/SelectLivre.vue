<template>
  <div>
    <input v-model="select" type="checkbox" v-on:click="setSelect()"/>
    <a>{{ book }}</a>
  </div>
</template>

<script>
export default {
  name: "SelectLivre",
  props:['book'],
  data() {
    return {
      select: false
    }
  },
  mounted() {
    if(sessionStorage.getItem(this.book) !== null) {
      this.select = true;
    } else {
      this.select = false;
    }
  },
  methods: {
    setSelect() {
      if(this.select) {
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