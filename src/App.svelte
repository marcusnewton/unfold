<script>
  import ApolloClient, { gql } from "apollo-boost";
  import { query, setClient } from "svelte-apollo";
  import Post, { p_gql } from "./components/Post.svelte";
  import Comment, { c_gql } from "./components/Comment.svelte";
  const client = new ApolloClient({
    uri: "https://unfold-gql.herokuapp.com/v1/graphql"
  });
  setClient(client);
  const posts = query(client, { query: gql(p_gql) });
  console.log(posts);
  const comments = query(client, { query: gql(c_gql) });
  console.log(comments);
</script>

<section>
  <Post />
   {p_gql}
  <ul>
    {#await $posts}
      <li>Loading...</li>
    {:then result}
      {#each result.data.post as post (post.uuid)}
        <li>{post.title}</li>
      {:else}
        <li>No posts found</li>
      {/each}
    {:catch error}
      <li>Error loading posts: {error}</li>
    {/await}
  </ul>
  <Comment />
   {c_gql}
  <ul>
    {#await $comments}
      <li>Loading...</li>
    {:then result}
      {#each result.data.comment as comment (comment.uuid)}
        <li>{comment.text}</li>
      {:else}
        <li>No comments found</li>
      {/each}
    {:catch error}
      <li>Error loading comments: {error}</li>
    {/await}
  </ul>
</section>
