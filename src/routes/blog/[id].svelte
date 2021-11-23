<script lang="ts">
  import { page } from "$app/stores";
  import supabase from "$lib/db";
  import { onMount } from "svelte";

  type Post = {
    id: number;
    created_at: Date;
    title: string;
    content: string;
    author_id: number;
  };

  let post: Post;
  let contentParagraphs: string[];
  onMount(async () => {
    let postResponse = await supabase
      .from("Posts")
      .select("*")
      .eq("id", $page.params.id)
      .single();
    if (postResponse && !postResponse.error) {
      post = postResponse.data;
      contentParagraphs = postResponse.data.content
        .split("\n")
        .filter((p) => p.length > 0);
      console.log(contentParagraphs);
    }
  });

  const options: Intl.DateTimeFormatOptions = {
    year: "numeric",
    month: "short",
    day: "numeric",
  };
</script>

<div class="post">
  {#if post}
    <h2>{post.title}</h2>
    <p>
      {post.author_id} : {new Date(post.created_at).toLocaleDateString(
        undefined,
        options
      )}
    </p>
    {#each contentParagraphs as paragraph}
      <p class="content">{paragraph}</p>
    {/each}
  {/if}
</div>

<style>
  .post {
    width: 80%;
    margin: auto;
    display: flex;
    flex-direction: column;
    align-items: center;
  }

  .content {
    width: 100%;
    text-align: left;
    text-indent: 50px;
    margin: 8px 0;
  }
</style>
