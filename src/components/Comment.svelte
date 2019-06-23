<script context="module">
  export const c_gql = `
    comments {
      uuid
      text
      author {
        name
      }
    }
`;
</script>

<script>
  export let data;
</script>

<div class="content box">
  <p>
    <strong>{data.author.name}</strong>
    <br />
     {data.text}
  </p>
</div>
