<script>
  import { onMount } from "svelte";
  import * as d3 from "d3";

  let width = 940; // Scale the width to 940 pixels for visibility (1 foot = 10 pixels)
  let height = 940 * (50 / 94); // Scale the height proportionally to the width based on court dimensions

  onMount(() => {
    drawCourt();
  });

  function drawCourt() {
    const svg = d3.select("#court")
      .attr("width", width)
      .attr("height", height);

    const xScale = d3.scaleLinear()
      .domain([0, 94]) // NBA court length is 94 feet
      .range([0, width]);

    const yScale = d3.scaleLinear()
      .domain([0, 50]) // NBA court width is 50 feet
      .range([height, 0]);

    svg.append("rect")
      .attr("x", xScale(0)) // x position, scaled
      .attr("y", yScale(50)) // y position, scaled
      .attr("width", xScale(94)) // width of the court, scaled
      .attr("height", yScale(0) - yScale(50)) // height of the court, scaled
      .style("fill", "none") // no fill color
      .style("stroke", "black") // black border
      .style("stroke-width", 2); // border width

    // Draw center circle
    svg.append("circle")
      .attr("cx", xScale(47))
      .attr("cy", yScale(25))
      .attr("r", yScale(19) - yScale(25)) // radius scaled
      .style("fill", "none")
      .style("stroke", "black")
      .style("stroke-width", 2);
 
  }
</script>

<svg id="court"></svg>

<style>
</style>
