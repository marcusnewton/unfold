<script>
  import ApolloClient, { gql } from "apollo-boost";
  import { query, setClient } from "svelte-apollo";

  import Post, { p_gql } from "./components/Post.svelte";
  import Comment, { c_gql } from "./components/Comment.svelte";
  const client = new ApolloClient({
    uri: "https://unfold-gql.herokuapp.com/v1/graphql"
  });
  setClient(client);
  const queryQL = `
    {
      post(where: {uuid: {_eq: "35c96e5b-e5a5-4cf0-ac27-27c684864aca"}}) {
        ${p_gql}
        ${c_gql}
      }
    }
  `;
  const data = query(client, {
    query: gql(queryQL)
  });
  console.log(JSON.stringify(data.result));
</script>

<svelte:head>
  <link
    rel="stylesheet"
    href="https://cdnjs.cloudflare.com/ajax/libs/bulma/0.7.5/css/bulma.min.css" />
</svelte:head>

<section class="section">
  <div class="container">
    {#await $data}
      <p>Loading...</p>
    {:then result}
      <Post data={result.data.post[0]} />
      {#each result.data.post[0].comments as comment (comment.uuid)}
        <Comment data={comment} />
      {/each}
    {:catch error}
      <p>Error loading posts: {error}</p>
    {/await}
  </div>
</section>
