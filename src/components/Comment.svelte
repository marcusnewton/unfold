<script context="module">
  export const c_gql = `
    fragment Comment on post {
      comments {
        uuid
        text
        author {
          name
        }
      }
    }
`;
</script>

<script>
  export let data;
</script>

<p>{data.text}</p>
