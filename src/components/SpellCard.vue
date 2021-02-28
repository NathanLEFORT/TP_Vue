<template>
  <div class="card">
    <div class="card-header" v-on:click="close()">{{spell[1]}} - Click to close</div>
    <div class="card-body">
      <div class="row"><p><b>School : </b>{{spell[2]}}</p></div>
      <div class="row"><p><b>Branches : </b>{{spell[3].join(", ")}}</p></div>
      <div class="row"><p><b>Classes : </b>{{this.getClasses().join(", ")}}</p></div>
      <div class="row"><p><b>Components : </b>{{spell[5].join(", ")}}</p></div>
      <div class="row"><p><b>Action : </b>{{spell[6]}}</p></div>
      <div class="row"><p><b>Distance : </b>{{spell[7]}}</p></div>
      <div class="row"><p><b>Effect : </b>{{spell[8].substr(7)}}</p></div>
      <div class="row"><p><b>Duration : </b>{{spell[9]}}</p></div>
      <div class="row"><p><b>Saving Throw : </b>{{spell[10]}}</p></div>
      <div class="row"><p><b>Spell Resistance : </b>{{spell[11]}}</p></div>
      <div class="row"><p><b>Description : </b>{{spell[12]}}</p></div>
      <div class="row"><p><b>Needed : </b>{{spell[13]}}</p></div>
    </div>
  </div>
</template>

<script>
export default {
  name: "SpellCard",
  props: ['spell'],
  methods : {
    close(){
      this.$parent.showList();
    },

    getClasses(){
      let classes = [];
      this.spell[4].forEach(element => {
        let classString = element[0]+" "+element[1];
        classes.push(classString);
      });
      return classes;
    }
  }
}
</script>

<style scoped>

</style>