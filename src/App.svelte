<script>
  let search = "";
  let isLoading = false;
  const API_URL =
    "https://api.giphy.com/v1/gifs/search?api_key=JnxTmEGKXjZeUKBzRjTQoMDg8OX8pS5U&rating=pg&q=";

  let gifs = [];

  async function formSubmitted(event) {
	isLoading = true;
	gifs = [];
    const url = `${API_URL}${search}`;
    const response = await fetch(url);
    const json = await response.json();
    gifs = json.data.map(gif => gif.images.fixed_height.url);
    isLoading = false;
  }
</script>

<style>
  .results {
    column-count: 3;
  }
  img {
    width: 100%;
    height: auto;
  }
  main {
    text-align: center;
    padding: 1em;
    max-width: 240px;
    margin: 0 auto;
  }

  h1 {
    color: #ff3e00;
    text-transform: uppercase;
    font-size: 4em;
    font-weight: 100;
  }

  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }
</style>

<main>
  <form on:submit|preventDefault={formSubmitted}>
    <label for="search">Search</label>
    <input bind:value={search} id="search" name="search" />
    <button type="submit">GO</button>
  </form>

  {#if isLoading}
    <img
      alt="isloading"
      src="https://media.giphy.com/media/3osxY5p129OPafgkw0/giphy.gif" />
  {/if}

  <div class="results">
    {#each gifs as gif}
      <img alt="gif" src={gif} />
    {/each}
  </div>
</main>
