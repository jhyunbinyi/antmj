<script>
  import Meta from "./Meta.svelte";
  import Title from "./Components/Title.svelte";
  import Intro from "./Components/Intro.svelte";
  import TextOne from "./Components/TextOne.svelte";
  import LineChart from "./Components/LineChart.svelte";
  import Conclusion from "./Components/Conclusion.svelte";
  import Resources from "./Components/Resources.svelte";
  import Shotchart from "./Components/Shotchart.svelte";
  import TextTwo from "./Components/TextTwo.svelte";
  import TextThree from "./Components/TextThree.svelte";

  import { onMount } from "svelte";
  
  let text = "Like Father Like Son?";
  let letters = [];

  onMount(() => {
    letters = text.split("");
  });
</script>

<style>
  @import url('https://fonts.googleapis.com/css2?family=Staatliches&display=swap');

  body {
    font-family: 'Staatliches', sans-serif;
  }

  .taskbar {
    position: relative;
    width: 100%;
    background: url('/mjdunk.gif') no-repeat center center fixed;
    background-size: cover;
    color: white;
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 360px;
    font-size: 1.5em;
    font-family: 'Staatliches', sans-serif;
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
    font-family: 'Staatliches', sans-serif;
    text-shadow: 4px 4px 8px rgba(0, 0, 0, 0.7);
  }

  .taskbar span {
    display: inline-block;
    animation: hover 3s ease-in-out infinite;
    transform: translateX(-2px); /* Offset text horizontally */
  }

  @keyframes hover {
    0%, 100% {
      transform: translateY(0) translateX(-2px); /* Maintain horizontal offset */
    }
    50% {
      transform: translateY(-3px) translateX(-2px); /* Maintain horizontal offset */
    }
  }
</style>

<Meta />
<div class="taskbar">
  <p>
    {#each letters as letter, i}
      <span style="animation-delay: {i * 0.1}s">{letter}</span>
    {/each}
  </p>
</div>
<Title />
<Intro />
<TextOne />
<Shotchart />
<TextTwo />
<LineChart />
<TextThree />
<Conclusion />
<Resources />