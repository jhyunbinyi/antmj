<section id="resources">
  <h3 class="body-header">References + Open Source</h3>
  <p class="body-text">
    This article is a product of the following resources:
    <br /><br />
  </p>
  <div class="resource-list">
    <p class="resource-item">
      <a class="on-end" href="https://d3js.org/">D3.js</a>
      <span>(Mike Bostock & Philippe Rivière)</span>
    </p>
    <p class="resource-item">
      <a class="on-end" href="https://layercake.graphics/">LayerCake</a>
      <span>(Michael Keller)</span>
    </p>
    <p class="resource-item">
      <a class="on-end" href="https://svelte.dev/">Svelte</a>
      <span>(Rich Harris)</span>
    </p>
  </div>
</section>

<style>
  @keyframes gradient {
    0% {
      background-position: 0% 50%;
    }
    50% {
      background-position: 100% 50%;
    }
    100% {
      background-position: 0% 50%;
    }
  }

  #resources {
    padding: 2rem 1rem;
    background: linear-gradient(270deg, #04052E, #540B0E);
    background-size: 400% 400%;
    animation: gradient 15s ease infinite;
    color: white;
  }

  .resource-list {
    max-width: 600px;
    margin: 0 auto;
    text-align: left;
  }

  .resource-item {
    margin-bottom: 1rem;
    font-size: 1.125rem;
    line-height: 1.5em;
  }

  a.on-end {
    text-decoration: underline;
    color: #f1f3f3;
  }

  @media screen and (max-width: 950px) {
    .resource-list {
      max-width: 80%;
    }

    .resource-item {
      font-size: 1rem;
    }
  }
</style>
