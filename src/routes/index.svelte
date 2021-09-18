<script lang="ts">
  import { onMount } from "svelte";

  type Pokemon = {
    name: string;
    url: string;
  };
  let items: Pokemon[] = [];

  onMount(async () => {
    let itemsResponse = await fetch(
      "https://pokeapi.co/api/v2/pokemon?limit=10"
    );
    let itemsJson: { results: Pokemon[] } = await itemsResponse.json();
    items = itemsJson.results;
  });
</script>

<h1>Welcome to the Store</h1>
<h3>Featured Items:</h3>
<ul>
  {#if items}
    {#each items as item, i}
      <p>{item.name}</p>
      <img
        src={`https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/${
          i + 1
        }.png`}
        alt={item.name}
      />
    {/each}
  {/if}
</ul>
