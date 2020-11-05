<!-- Use preprocessors via the lang attribute! e.g. <template lang="pug"> -->
<template>
  <div id="app">
    <div class="view">
      <p>test</p>
      <chartxkcd-line :config="config" class="view"></chartxkcd-line>
    </div>
    <button>Say hello.</button>
  </div>
</template>
<script>
import { chartXKCDLine } from 'chart.xkcd-vue'

 export default {
   name: 'app',
   data() {
     return {
       dt: {},
       blr: [],
       config: {
         title: 'Covid 19 | Belarus',
         xLabel: 'Date',
         yLabel: 'Mens',
         data: {
           labels: [],
           datasets: [
             {
               label: 'Plan',
               data: []
             },
             {
               label: 'Reality',
               data: []
             },
             {
               label: 'Test #1',
               data: [] //[2124, 2245, 1112, 2270, 2280, 3356, 4140, 2380, 3200, 2125]
             }
           ]
         }
       }
     }
   },
   components: {
     'chartxkcd-line': chartXKCDLine
   },
   methods: {
     changeData () {
       var xhr = new XMLHttpRequest();
      //posts list
      xhr.open("GET", "https://pomber.github.io/covid19/timeseries.json", false);
      xhr.send();

      this.dt =  window.JSON.parse(xhr.responseText);
      this.blr  = this.dt.Belarus;
      this.config.data.datasets[0].label = 'Confirmed';
      this.config.data.datasets[1].label = 'Deaths';
      this.config.data.datasets[2].label = 'Recovered';
      for(let i=0; i<this.blr.length; i++) {
         if(this.blr[i].deaths>0) {
           this.config.data.labels.push(this.blr[i].date);
           this.config.data.datasets[0].data.push(this.blr[i].confirmed);
           this.config.data.datasets[1].data.push(this.blr[i].deaths);
           this.config.data.datasets[2].data.push(this.blr[i].recovered);
         }
      }/*
      for(let i=30; i<this.blr.length; i+=2) {
        this.config.data.labels.push(this.blr[i].date);
      }*/
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
.view {
   width: 600px;
   height: 800px;
}

.tick text {
  opacity: 0;
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
