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
<ul class="flex-container">
  {#if items}
    {#each items as item, i}
      <div class="card">
        <span class="flex-item">{item.name}</span>
        <img
          class="flex-item"
          src={`https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/${
            i + 1
          }.png`}
          alt={item.name}
        />
      </div>
    {/each}
  {/if}
</ul>

<style>
  .flex-container {
    display: flex;
    flex-wrap: wrap;
    align-content: flex-start;
  }

  .card {
    flex: 1 0 25%;
    display: flex;
    justify-content: center;
    flex-direction: column;
    flex-grow: 0;
  }

  img {
    height: 100px;
    width: 100px;
  }

  .flex-item {
    align-self: center;
  }
</style>
