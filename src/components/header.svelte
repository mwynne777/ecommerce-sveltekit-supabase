<script lang="ts">
  export let path: string;
  console.log(path);
</script>

<div class="header">
  <a href="#" class="logo">Pokemon Store</a>
  <div class="header-pages">
    <a href="/" class:active={path === "/"}>Home</a>
    <a href="/search" class:active={path === "/search"}>Search</a>
  </div>
</div>

<style>
  .header {
    background-color: #f1f1f1;
    padding: 24px 16px;
  }

  .header a:hover {
    background-color: #ddd;
    color: black;
  }

  .header a.active {
    background-color: dodgerblue;
    color: white;
  }

  .header-pages {
    float: right;
  }

  .header-pages a {
    margin: 0 8px;
    color: black;
    text-align: center;
    padding: 8px 8px;
    text-decoration: none;
    font-size: 16px;
    border-radius: 4px;
  }
</style>
