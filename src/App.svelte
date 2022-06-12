<script>
  import logo from "./assets/Poisnoed Dragon Silver Green..orange..png";
  import Counter from "./lib/Counter.svelte";
  ///
  const BLACKBUTLER_API_ROOT = "http://localhost:9000/api";
  const SAY_ENDPOINT = `${BLACKBUTLER_API_ROOT}/say/`;
  ///
  var say_text = "Iced tea is awful ;)";
  var say_res_promise;

  function say_click(event) {
    say_res_promise = fetch(SAY_ENDPOINT, {
      method: "POST",
      headers: {
        Accept: "application/json",
        "Content-Type": "application/json",
      },
      body: JSON.stringify({ text: say_text }),
    }).then((response) => response.json());
  }
  ///
</script>

<main>
  <img class="img_round" src={logo} alt="Svelte Logo" />
  <h1 class="title">SEED</h1>

  <div class="grid_main">
    <Counter />

    <input bind:value={say_text} />

    <button on:click={say_click}>Say me!</button>

    {#if say_res_promise}
      {#await say_res_promise}
        <p>Waiting ...</p>
      {:then say_res}
        <p>retcode: {say_res.retcode}</p>
      {/await}
    {/if}
  </div>
</main>

<style>
  :root {
    font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Oxygen,
      Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serif;
  }

  main {
    text-align: center;
    padding: 1em;
    margin: 0 auto;
  }

  .grid_main {
    display: grid;
    grid-row-gap: 30px;
    justify-items: center;
    justify-content: center;
  }

  img {
    height: 16rem;
    width: 16rem;
  }

  h1 {
    color: #ff3e00;
    text-transform: uppercase;
    font-size: 4rem;
    font-weight: 100;
    line-height: 1.1;
    margin: 2rem auto;
    max-width: 14rem;
  }

  .title {
    color: aquamarine;
  }

  .img_round {
    border-radius: 50%;
  }

  p {
    max-width: 14rem;
    margin: 1rem auto;
    line-height: 1.35;
  }

  @media (min-width: 480px) {
    h1 {
      max-width: none;
    }

    p {
      max-width: none;
    }
  }
</style>
