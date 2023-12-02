<template>
  <p><b>{{ url }}</b></p>

  <div :id="'treemap-' + index" class="svg-container"></div>
</template>

<script>
import { defineComponent } from 'vue'
import * as d3 from 'd3'

export default defineComponent({
  props: ['colorData', 'url', 'index'],
  updated () {
    // Clear the treemap
    d3.select(`#treemap-${this.index}`).selectAll('*').remove()

    const width = 1200
    const height = 800

    // Create the SVG element
    const svg = d3.select(`#treemap-${this.index}`)
      .append('svg')
      .attr('preserveAspectRatio', 'xMinYMin meet')
      .attr('viewBox', `0 0 ${width} ${height}`)
      .classed('svg-content', true)

    // Create a hierarchical data structure
    const root = d3.hierarchy({ children: this.colorData })
      .sum(function (d) { return d.value })

    const treemap = d3.treemap()
      .size([width, height])

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
      // Add a border to make sure the colors don't conflict w/ the background
      .style('stroke', 'black')
      .style('stroke-width', '0.5px')
      .append('title').text(d => d.data.color)
  }
})
</script>
<style>
.svg-container {
  display: inline-block;
  position: relative;
  width: 75%;
  padding-bottom: 75%;
  vertical-align: top;
  float: center;
  overflow: hidden;
}
.svg-content {
  display: inline-block;
  position: absolute;
  top: 0;
  left: 0;
}
</style>
