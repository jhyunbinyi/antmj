<script>
  import Meta from "./Meta.svelte";
  import Title from "./Components/Title.svelte";
  import Intro from "./Components/Intro.svelte";
  import TextAndMathEquations from "./Components/TextAndMathEquations.svelte";
  import LineChart from "./Components/LineChart.svelte";
  import Conclusion from "./Components/Conclusion.svelte";
  import Resources from "./Components/Resources.svelte";
  import Shotchart from "./Components/Shotchart.svelte";
</script>

<style>
  @import url('https://fonts.googleapis.com/css2?family=Bebas+Neue&display=swap');

  body {
    font-family: 'Bebas Neue', sans-serif;
  }

  .taskbar {
    position: relative;
    width: 100%;
    background: url('./mjdunk.gif') no-repeat center center fixed;
    background-size: cover;
    color: white;
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 360px;
    font-size: 1.5em;
    font-family: 'Bebas Neue', sans-serif;
  }

  .taskbar::before {
    content: '';
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background: inherit;
    filter: blur(4px);
    z-index: 1;
  }

  .taskbar p {
    position: relative;
    z-index: 2;
    font-size: 1.6em;
    font-family: 'Bebas Neue', sans-serif;
    text-shadow: 4px 4px 8px rgba(0, 0, 0, 0.7);
  }

  .taskbar a {
    position: relative;
    z-index: 2;
    color: white;
    margin: 0 10px;
    text-decoration: none;
    font-family: 'Bebas Neue', sans-serif;
  }

  .taskbar a:hover {
    text-decoration: underline;
  }
</style>

<Meta />
<div class="taskbar">
  <p>Like Father Like Son?</p>
</div>
<Title />
<Intro />
<TextAndMathEquations />
<LineChart />
<Shotchart />
<Conclusion />
<Resources />