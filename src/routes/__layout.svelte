<script context="module">
  /**
   * @type {import('@sveltejs/kit').Load}
   */
  export const load = async ({ page: { path } }) => ({
    props: {
      path,
    },
  });
</script>

<script lang="ts">
  import Header from "../components/header.svelte";

  export let path: string;
</script>

<Header {path} />
<div class="page-body">
  <slot />
</div>

<style>
  :global(body) {
    margin: 0;
  }

  .page-body {
    margin: 8px;
  }
</style>
