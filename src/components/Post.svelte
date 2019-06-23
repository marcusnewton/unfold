<script context="module">
  export const p_gql = `
    fragment Post on post {
      title
      date
      body
    }
`;
</script>

<script>
  export let data;
</script>

<h1>{data.title}</h1>
