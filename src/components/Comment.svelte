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

<p>{data.text}</p>
