<script>
  import { onMount } from "svelte";
  import { select } from "d3-selection";
  import { scaleBand, scaleLinear } from "d3-scale";
  import { axisBottom, axisLeft } from "d3-axis";

  let width = 800;
  let height = 500;
  const margin = { top: 20, right: 30, bottom: 40, left: 70 };

  const leagueAvgMJ = [108.7, 109.3, 104.8, 105.0];
  const leagueAvgAnt = [112.1, 115.4, 115.1, 112.1];

  const rawData = {
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

  const normalizedData = {
    mj: [
      { year: "Year 1", ppg: (28.2 / leagueAvgMJ[0]) * 100 },
      { year: "Year 2", ppg: (22.7 / leagueAvgMJ[1]) * 100 },
      { year: "Year 3", ppg: (37.1 / leagueAvgMJ[2]) * 100 },
      { year: "Year 4", ppg: (35.0 / leagueAvgMJ[3]) * 100 },
    ],
    ant: [
      { year: "Year 1", ppg: (19.3 / leagueAvgAnt[0]) * 100 },
      { year: "Year 2", ppg: (21.3 / leagueAvgAnt[1]) * 100 },
      { year: "Year 3", ppg: (24.6 / leagueAvgAnt[2]) * 100 },
      { year: "Year 4", ppg: (25.9 / leagueAvgAnt[3]) * 100 },
    ],
  };

  let normalized = false;

  function getData() {
    return normalized ? normalizedData : rawData;
  }

  const years = ["Year 1", "Year 2", "Year 3", "Year 4"];

  function updateChart() {
    const svg = select("#chart");
    svg.selectAll("*").remove();

    const data = getData();

    const xScale = scaleBand()
      .domain(years)
      .range([0, width - margin.left - margin.right])
      .padding(0.2);

    const yScale = scaleLinear()
      .domain([0, Math.max(...data.mj.map(d => d.ppg), ...data.ant.map(d => d.ppg))])
      .nice()
      .range([height - margin.top - margin.bottom, 0]);

    const g = svg
      .attr("width", width)
      .attr("height", height)
      .append("g")
      .attr("transform", `translate(${margin.left},${margin.top})`);

    g.append("g")
      .attr("transform", `translate(0,${height - margin.top - margin.bottom})`)
      .call(axisBottom(xScale));

    g.append("g")
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

    g.selectAll(".bar.mj")
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
        tooltip.style("visibility", "visible").text(`${normalized ? 'Normalized ' : ''}PPG: ${d.ppg.toFixed(2)}`);
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

    g.selectAll(".bar.ant")
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
        tooltip.style("visibility", "visible").text(`${normalized ? 'Normalized ' : ''}PPG: ${d.ppg.toFixed(2)}`);
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

    g.append("text")
      .attr("class", "y-label")
      .attr("transform", "rotate(-90)")
      .attr("y", -margin.left + 20)
      .attr("x", -height / 2 + margin.top)
      .attr("dy", "1em")
      .attr("text-anchor", "middle")
      .text(normalized ? "Percentage of Team Points Scored" : "Points Per Game (PPG)");

    // Legend
    const legend = g.append("g")
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
  }

  onMount(() => {
    updateChart();
  });

  $: if (normalized !== undefined) {
    updateChart();
  }
</script>

<h1 style="text-align: center; margin: 0 0 30px;">
  Early Career Scoring Comparison
</h1>

<div class="container">
  <div class="chart-container">
    <div class="checkbox-container">
      <input type="checkbox" id="normalize" bind:checked={normalized} />
      <label for="normalize">Normalize Data</label>
    </div>
    <svg id="chart"></svg>
  </div>
</div>

<style>
  .container {
    display: flex;
    flex-direction: column;
    align-items: center;
  }

  .chart-container {
    position: relative;
    display: flex;
    flex-direction: column;
    align-items: center;
  }

  .checkbox-container {
    display: flex;
    align-items: center;
    margin-bottom: 10px;
    position: absolute;
    top: -30px; /* Adjust this value to move the checkbox up/down */
    left: 70px; /* Align with the y-axis */
  }

  .checkbox-container input[type="checkbox"] {
    appearance: none;
    width: 16px;
    height: 16px;
    border: 1px solid #000;
    border-radius: 2px;
    margin-right: 8px;
    cursor: pointer;
  }

  .checkbox-container input[type="checkbox"]:checked {
    background-color: #000;
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