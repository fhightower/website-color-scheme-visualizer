<template>
  <div class="form">
    <form>
      <input type="text" placeholder="Enter URL here..." id="url" v-model="url">
      <input type="submit" @click="processURL">
    </form>

    <div id="treemap"></div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import axios from 'axios'
import * as d3 from 'd3'

const processingUrl = ''

export default defineComponent({
  data () {
    return {
      url: ''
    }
  },
  methods: {
    processURL () {
      console.log(this.url)
      this.drawResults()
      /*
      axios.post(processingUrl, {
        url: this.url
      })
        .then(function (response) {
          console.log(response)
          this.drawResults(response)
        })
        .catch(function (error) {
          console.error(error)
        })
      */
    },
    drawResults () {
      console.log('a')
      const data = [
        { color: '#fff', value: 67.677 },
        { color: '#8a2be2', value: 20.8 },
        { color: '#191970', value: 3.4 }
      ]

      // const svgContainer = document.getElementById('svg-container')
      // Append the 'chart' SVG to the container element
      // svgContainer.appendChild(chart)
      // Set up the dimensions for the treemap
      const width = 600
      const height = 400

      // Create the SVG element
      const svg = d3.select('#treemap')
        .append('svg')
        .attr('width', width)
        .attr('height', height)

      // Create a hierarchical data structure
      const root = d3.hierarchy({ children: data })
        .sum(function (d) { return d.value })

      // Create the treemap layout
      const treemap = d3.treemap()
        .size([width, height])

      // Compute the treemap layout
      treemap(root)

      // Create rectangles for each data point
      const nodes = svg.selectAll('.node')
        .data(root.leaves())
        .enter()
        .append('g')
        .attr('class', 'node')
        .attr('transform', function (d) { return 'translate(' + d.x0 + ',' + d.y0 + ')' })

      nodes.append('rect')
        .attr('width', function (d) { return d.x1 - d.x0 })
        .attr('height', function (d) { return d.y1 - d.y0 })
        .style('fill', function (d) { return d.data.color })

      // Add text labels
      nodes.append('text')
        .attr('x', 5)
        .attr('y', 15)
        .text(function (d) { return d.data.value })
    }
  },
  name: 'URLInput'
})
</script>

  <!-- Add "scoped" attribute to limit CSS to this component only -->
  <style scoped>
  </style>
