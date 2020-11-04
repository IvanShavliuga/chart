<!-- Use preprocessors via the lang attribute! e.g. <template lang="pug"> -->
<template>
  <div id="app">
    <p>
      Learn more with the
      <a
        href="https://vuejs.org/"
        target="_blank"
        rel="noopener"
      >Vue Docs &amp; Resources</a>.
    </p>
    <div class="view">
      <p>test</p>
      <chartxkcd-line :config="config" class="view"></chartxkcd-line>
    </div>
    <button @click="doSomething">Say hello.</button>
  </div>
</template>

<script>
import { chartXKCDLine } from 'chart.xkcd-vue'

 export default {
   name: 'app',
   data() {
     return {
       config: {
         title: 'Monthly income of an indie developer',
         xLabel: 'Month',
         yLabel: '$ Dollors',
         data: {
           labels: ['1', '2', '3', '4', '5', '6', '7', '8', '9', '10'],
           datasets: [
             {
               label: 'Plan',
               data: [30, 70, 200, 300, 500, 800, 1500, 2900, 5000, 8000]
             },
             {
               label: 'Reality',
               data: [0, 1, 30, 70, 80, 100, 50, 80, 40, 150]
             }
           ]
         }
       }
     }
   },
   components: {
     'chartxkcd-line': chartXKCDLine
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
   width: 400px;
   height: 400px;
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
