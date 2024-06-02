<script>
  import { onMount } from "svelte";
  import { select } from "d3-selection";
  import { scaleBand, scaleLinear } from "d3-scale";
  import { axisBottom, axisLeft } from "d3-axis";

  let width = 800;
  let height = 500;
  const margin = { top: 20, right: 30, bottom: 40, left: 70 };

  const data = {
    mj: [
      { year: "Year 1", ppg: 28.2 },
      { year: "Year 2", ppg: 22.7 },
      { year: "Year 3", ppg: 37.1 },
      { year: "Year 4", ppg: 35.0 },
    ],
    ant: [
      { year: "Year 1", ppg: 19.3 },
      { year: "Year 2", ppg: 21.3 },
      { year: "Year 3", ppg: 24.6 },
      { year: "Year 4", ppg: 25.9 },
    ],
  };

  const years = ["Year 1", "Year 2", "Year 3", "Year 4"];

  onMount(() => {
    const svg = select("#chart")
      .attr("width", width)
      .attr("height", height)
      .append("g")
      .attr("transform", `translate(${margin.left},${margin.top})`);

    const xScale = scaleBand()
      .domain(years)
      .range([0, width - margin.left - margin.right])
      .padding(0.2);

    const yScale = scaleLinear()
      .domain([0, Math.max(...data.mj.map(d => d.ppg), ...data.ant.map(d => d.ppg))])
      .nice()
      .range([height - margin.top - margin.bottom, 0]);

    svg.append("g")
      .attr("transform", `translate(0,${height - margin.top - margin.bottom})`)
      .call(axisBottom(xScale));

    svg.append("g")
      .call(axisLeft(yScale));

    const tooltip = select("body")
      .append("div")
      .attr("class", "tooltip")
      .style("position", "absolute")
      .style("visibility", "hidden")
      .style("background", "#f9f9f9")
      .style("border", "1px solid #d3d3d3")
      .style("padding", "8px")
      .style("border-radius", "4px")
      .style("font-size", "12px")
      .style("color", "#333");

    svg.selectAll(".bar.mj")
      .data(data.mj)
      .enter()
      .append("rect")
      .attr("class", "bar mj")
      .attr("x", d => xScale(d.year))
      .attr("y", d => yScale(d.ppg))
      .attr("width", xScale.bandwidth() / 2)
      .attr("height", d => height - margin.top - margin.bottom - yScale(d.ppg))
      .attr("fill", "#CE1141")
      .on("mouseover", function (event, d) {
        tooltip.style("visibility", "visible").text(`PPG: ${d.ppg}`);
        select(this).attr("fill", "#E57373");
      })
      .on("mousemove", function (event) {
        tooltip
          .style("top", `${event.pageY - 10}px`)
          .style("left", `${event.pageX + 10}px`);
      })
      .on("mouseout", function () {
        tooltip.style("visibility", "hidden");
        select(this).attr("fill", "#CE1141");
      });

    svg.selectAll(".bar.ant")
      .data(data.ant)
      .enter()
      .append("rect")
      .attr("class", "bar ant")
      .attr("x", d => xScale(d.year) + xScale.bandwidth() / 2)
      .attr("y", d => yScale(d.ppg))
      .attr("width", xScale.bandwidth() / 2)
      .attr("height", d => height - margin.top - margin.bottom - yScale(d.ppg))
      .attr("fill", "#0C2340")
      .on("mouseover", function (event, d) {
        tooltip.style("visibility", "visible").text(`PPG: ${d.ppg}`);
        select(this).attr("fill", "#90A4AE");
      })
      .on("mousemove", function (event) {
        tooltip
          .style("top", `${event.pageY - 10}px`)
          .style("left", `${event.pageX + 10}px`);
      })
      .on("mouseout", function () {
        tooltip.style("visibility", "hidden");
        select(this).attr("fill", "#0C2340");
      });

    svg.append("text")
      .attr("class", "y-label")
      .attr("transform", "rotate(-90)")
      .attr("y", -margin.left + 20)
      .attr("x", -height / 2 + margin.top)
      .attr("dy", "1em")
      .attr("text-anchor", "middle")
      .text("Points Per Game (PPG)");

    // Legend
    const legend = svg.append("g")
      .attr("transform", `translate(${width - margin.right - 150},${margin.top})`);

    legend.append("rect")
      .attr("x", 0)
      .attr("y", 0)
      .attr("width", 18)
      .attr("height", 18)
      .style("fill", "#CE1141");

    legend.append("text")
      .attr("x", 24)
      .attr("y", 9)
      .attr("dy", ".35em")
      .text("Michael Jordan");

    legend.append("rect")
      .attr("x", 0)
      .attr("y", 24)
      .attr("width", 18)
      .attr("height", 18)
      .style("fill", "#0C2340");

    legend.append("text")
      .attr("x", 24)
      .attr("y", 33)
      .attr("dy", ".35em")
      .text("Anthony Edwards");
  });
</script>

<h1 style="text-align: center; margin-top: 60px;">
  Rookie Year PPG Comparison
</h1>

<div class="container">
  <svg id="chart"></svg>
</div>

<style>
  .container {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
  }

  svg {
    font: 10px sans-serif;
  }

  .axis path,
  .axis line {
    fill: none;
    shape-rendering: crispEdges;
  }

  .axis text {
    font: 10px sans-serif;
  }

  .bar {
    fill-opacity: 0.7;
  }

  .bar:hover {
    fill-opacity: 1;
  }

  .y-label {
    font-size: 12px;
    font-weight: bold;
  }

  .tooltip {
    pointer-events: none;
  }
</style>
