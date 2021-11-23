<script lang="ts">
  import { onMount } from "svelte";

  type Pokemon = {
    name: string;
    url: string;
  };
  let items: Pokemon[] = [];

  onMount(async () => {
    let itemsResponse = await fetch(
      "https://pokeapi.co/api/v2/pokemon?limit=15"
    );
    let itemsJson: { results: Pokemon[] } = await itemsResponse.json();
    items = itemsJson.results;
  });
</script>

<h1>Welcome to the Store</h1>
<h3>Featured Items:</h3>
<ul class="grid-container">
  {#if items}
    {#each items as item, i}
      <div class="card">
        <img
          class="flex-item"
          src={`https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/${
            i + 1
          }.png`}
          alt={item.name}
        />
        <hr />
        <span class="flex-item card-title">{item.name}</span>
      </div>
    {/each}
  {/if}
</ul>

<style>
  .grid-container {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
    grid-column-gap: 10px;
    row-gap: 32px;
  }

  .card {
    display: flex;
    flex-direction: column;
    border: 1px solid #f1f1f1;
  }

  img {
    height: 100px;
    width: 100px;
  }

  .flex-item {
    align-self: center;
  }

  hr {
    margin-left: 0;
    margin-right: 0;
    border: none;
    height: 1px;
    color: #f1f1f1;
    background-color: #f1f1f1;
  }

  .card-title {
    margin-bottom: 8px;
  }
</style>
