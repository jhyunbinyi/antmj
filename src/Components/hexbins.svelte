<script>
  import { onMount } from "svelte";
  import * as d3 from "d3";

  export let shots = [];

  let width = 940;
  let height = 940 * (50 / 94);

  onMount(() => {
    plotShots(shots);
  });

  function plotShots(shots) {
    const svg = d3.select("#shots")
      .attr("width", width)
      .attr("height", height);

    const xScale = d3.scaleLinear()
      .domain([0, 94])
      .range([0, width]);

    const yScale = d3.scaleLinear()
      .domain([0, 50])
      .range([height, 0]);

    svg.selectAll("circle").remove(); // Clear existing shots

    // Plot each shot
    shots.forEach(shot => {
      svg.append("circle")
        .attr("cx", xScale(shot.x))
        .attr("cy", yScale(shot.y))
        .attr("r", 5)
        .style("fill", shot.made ? "green" : "red")
        .style("stroke", "black")
        .style("stroke-width", 1);
    });
  }
</script>

<svg id="shots"></svg>

<style>
  /* Add any styles if necessary */
</style>

