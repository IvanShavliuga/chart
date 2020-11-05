<template>
  <div class="view">
    <p>test</p>
    <chartxkcd-line :config="config" class="view"></chartxkcd-line>
  </div>
</template>
<script>
import { chartXKCDLine } from 'chart.xkcd-vue'
export default {
  props: {
    dataset: {
      type: Array,
      required: true
    },
    title: {
      type: String,
      required: true
    }
  },
  data () {
    return {
      config: {
      title: 'Covid 19 | Belarus',
      xLabel: 'Date',
      yLabel: 'Mens',
      data: {
        labels: [],
        datasets: [
          {
            label: 'Confirmed',
            data: []
          },
          {
            label: 'Deaths',
            data: []
          },
          {
            label: 'Recovered',
            data: []
          }
        ]
      }
    }}
  },
  created () {
    this.config.title = 'Covid 19 |' + this.title
    for(let i=0; i<this.dataset.length; i++) {
       this.config.data.labels.push(this.dataset[i].date);
       this.config.data.datasets[0].data.push(this.dataset[i].confirmed);
       this.config.data.datasets[1].data.push(this.dataset[i].deaths);
       this.config.data.datasets[2].data.push(this.dataset[i].recovered);
    }

  },
  updated () {
    this.config.title = 'Covid 19 |' + this.title
    for(let i=0; i<this.dataset.length; i++) {
       this.config.data.labels.push(this.dataset[i].date);
       this.config.data.datasets[0].data.push(this.dataset[i].confirmed);
       this.config.data.datasets[1].data.push(this.dataset[i].deaths);
       this.config.data.datasets[2].data.push(this.dataset[i].recovered);
    }
  },
  components: {
    'chartxkcd-line': chartXKCDLine
  }
}
</script>
<style>
.view {
   width: 600px;
   height: 800px;
}

.tick text {
  opacity: 0;
}
</style>
