<!-- Use preprocessors via the lang attribute! e.g. <template lang="pug"> -->
<template>
  <div id="app">

    <ul>
      <li v-for="(c, k) in countries"
        :key="k">
        <button @click="sel=c.id">{{c.id}}|{{c.country}}</button>
      </li>
    </ul>
    <Cartbox :title="countries[sel].country" :dataset="countries[sel].data"/>
    <button>Say hello.</button>
    <p>{{sel}}</p>
  </div>
</template>
<script>
import Cartbox from '@/components/Cartbox.vue'

 export default {
   name: 'app',
   data() {
     return {
       dt: {},
       blr: [],
       sel: 12,
       countries: []
     }
   },
   components: {
     Cartbox
   },
   methods: {
     changeData () {
       var xhr = new XMLHttpRequest();
      //posts list
      xhr.open("GET", "https://pomber.github.io/covid19/timeseries.json", false);
      xhr.send();
      this.dt =  window.JSON.parse(xhr.responseText);
      let i=0;
      for (let [key, val] of Object.entries(this.dt)) {
        this.countries.push({id: i, country: key, data: val});
        i++;
      }
    }
   },
   created() {
     this.changeData()
   }
 }
</script>

<!-- Use preprocessors via the lang attribute! e.g. <style lang="scss"> -->
<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}


a,
button {
  color: #4fc08d;
}

button {
  background: none;
  border: solid 1px;
  border-radius: 2em;
  font: inherit;
  padding: 0.75em 2em;
}
</style>
