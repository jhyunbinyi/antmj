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
  let words = [];

  onMount(() => {
    words = text.split(" ").map(word => {
      if (word.includes("Father")) {
        return { word, className: "father" };
      } else if (word.includes("Son")) {
        return { word, className: "son" };
      } else {
        return { word, className: "" };
      }
    });
  });
</script>

<style>
  @import url('https://fonts.googleapis.com/css2?family=Bebas+Neue&display=swap');

  body {
    font-family: 'Bebas Neue', sans-serif !important;
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
    font-size: 1.7em;
    font-family: 'Bebas Neue', sans-serif; /* Apply font to taskbar */
  }

  .taskbar::before {
    content: '';
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background: inherit;
    filter: blur(5px);
    z-index: 1;
  }

  .taskbar p {
    position: relative;
    z-index: 2;
    font-size: 1.6em;
    text-shadow: 4px 4px 8px rgba(0, 0, 0, 0.7);
    font-family: 'Bebas Neue', sans-serif; /* Apply font to taskbar paragraph */
  }

  .taskbar span {
    display: inline-block;
    margin-right: 2px; /* Adjust spacing between characters */
  }

  .father {
    color: #CE1141;
  }

  .son {
    color: #236192;
  }
</style>

<Meta />
<div class="taskbar">
  <p>
    {#each words as { word, className }, index}
      <span class={className}>{word}</span>{index < words.length - 1 ? ' ' : ''}
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
