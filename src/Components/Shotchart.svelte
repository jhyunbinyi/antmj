<script>
  import ShotPlot from './hexbins.svelte';
  import { onMount } from "svelte";
  import * as d3 from "d3";

  let width = 940; // Scale the width to 940 pixels for visibility (1 foot = 10 pixels)
  let height = 940 * (50 / 94); // Scale the height proportionally to the width based on court dimensions

  onMount(() => {
    drawCourt();
  });

    let shots = [
    { x: 47, y: 25, made: true },
    { x: 10, y: 15, made: false },
    { x: 20, y: 30, made: true },
    { x: 50, y: 20, made: false }
    // Add more shots as needed
  ];

  function drawCourt() {
    const svg = d3.select("#court")
      .attr("width", width)
      .attr("height", height);

    const xScale = d3.scaleLinear()
      .domain([0, 94])
      .range([0, width]);

    const yScale = d3.scaleLinear()
      .domain([0, 50])
      .range([height, 0]);

    // Draw the basketball court outline
    svg.append("rect")
      .attr("x", xScale(0)) // x position, scaled
      .attr("y", yScale(50)) // y position, scaled
      .attr("width", xScale(94)) // width of the court, scaled
      .attr("height", yScale(0) - yScale(50)) // height of the court, scaled
      .style("fill", "none") // no fill color
      .style("stroke", "black") // black border
      .style("stroke-width", 2); // border width

    // Draw the center circle
    svg.append("circle")
      .attr("cx", xScale(47))
      .attr("cy", yScale(25))
      .attr("r", xScale(6) - xScale(0))
      .style("fill", "none")
      .style("stroke", "black")
      .style("stroke-width", 2);

    // Draw the free throw circles
    svg.append("circle")
      .attr("cx", xScale(19))
      .attr("cy", yScale(25))
      .attr("r", xScale(6) - xScale(0))
      .style("fill", "none")
      .style("stroke", "black")
      .style("stroke-width", 2);

    svg.append("circle")
      .attr("cx", xScale(75))
      .attr("cy", yScale(25))
      .attr("r", xScale(6) - xScale(0)) 
      .style("fill", "none")
      .style("stroke", "black")
      .style("stroke-width", 2);
    
    svg.append("rect")
      .attr("x", xScale(75))
      .attr("y", yScale(34))
      .attr("width", xScale(19))
      .attr("height", yScale(32))
      .style("fill", "none")
      .style("stroke", "black")
      .style("stroke-width", 2);

    svg.append("rect")
      .attr("x", xScale(0))
      .attr("y", yScale(34))
      .attr("width", xScale(19))
      .attr("height", yScale(32))
      .style("fill", "none")
      .style("stroke", "black")
      .style("stroke-width", 2);

    svg.append("line")
      .attr("x1", xScale(4))
      .attr("y1", yScale(27))
      .attr("x2", xScale(4))
      .attr("y2", yScale(23))
      .style("stroke", "black")
      .style("stroke-width", 2);

    svg.append("line")
      .attr("x1", xScale(90))
      .attr("y1", yScale(27))
      .attr("x2", xScale(90))
      .attr("y2", yScale(23))
      .style("stroke", "black")
      .style("stroke-width", 2);

    svg.append("circle")
      .attr("cx", xScale(6))
      .attr("cy", yScale(25))
      .attr("r", xScale(1.8)) 
      .style("fill", "none")
      .style("stroke", "black")
      .style("stroke-width", 2);

    svg.append("circle")
      .attr("cx", xScale(88))
      .attr("cy", yScale(25))
      .attr("r", xScale(1.8)) 
      .style("fill", "none")
      .style("stroke", "black")
      .style("stroke-width", 2);

    svg.append("line")
      .attr("x1", xScale(0))
      .attr("y1", yScale(3))
      .attr("x2", xScale(14))
      .attr("y2", yScale(3))
      .style("stroke", "black")
      .style("stroke-width", 2);

    svg.append("line")
      .attr("x1", xScale(0))
      .attr("y1", yScale(47))
      .attr("x2", xScale(14))
      .attr("y2", yScale(47))
      .style("stroke", "black")
      .style("stroke-width", 2);

    svg.append("path")
      .attr("d", d3.arc()
        .innerRadius(xScale(23.75) - xScale(0))
        .outerRadius(xScale(23.75) - xScale(0))
        .startAngle(0.38)
        .endAngle(Math.PI / 1.134))
      .attr("transform", `translate(${xScale(5.25)}, ${yScale(25)})`)
      .style("fill", "none")
      .style("stroke", "black")
      .style("stroke-width", 2);

    svg.append("line")
      .attr("x1", xScale(80))
      .attr("y1", yScale(3))
      .attr("x2", xScale(94))
      .attr("y2", yScale(3))
      .style("stroke", "black")
      .style("stroke-width", 2);

    svg.append("line")
      .attr("x1", xScale(80))
      .attr("y1", yScale(47))
      .attr("x2", xScale(94))
      .attr("y2", yScale(47))
      .style("stroke", "black")
      .style("stroke-width", 2);

    svg.append("path")
      .attr("d", d3.arc()
        .innerRadius(xScale(23.75) - xScale(0))
        .outerRadius(xScale(23.75) - xScale(0))
        .startAngle(-0.38)
        .endAngle(-Math.PI / 1.134))
      .attr("transform", `translate(${xScale(88.75)}, ${yScale(25)})`)
      .style("fill", "none")
      .style("stroke", "black")
      .style("stroke-width", 2);

    // Draw the key areas
    svg.append("rect")
      .attr("x", xScale(17))
      .attr("y", yScale(19))
      .attr("width", xScale(19) - xScale(17))
      .attr("height", yScale(19) - yScale(0))
      .style("fill", "none")
      .style("stroke", "black")
      .style("stroke-width", 2);

    svg.append("rect")
      .attr("x", xScale(75))
      .attr("y", yScale(19))
      .attr("width", xScale(19) - xScale(17))
      .attr("height", yScale(19) - yScale(0))
      .style("fill", "none")
      .style("stroke", "black")
      .style("stroke-width", 2);

    // Draw the midcourt line
    svg.append("line")
      .attr("x1", xScale(47))
      .attr("y1", yScale(0))
      .attr("x2", xScale(47))
      .attr("y2", yScale(50))
      .style("stroke", "black")
      .style("stroke-width", 2);
  }
</script>

<svg id="court"></svg>
<ShotPlot {shots} />

<style>
</style>