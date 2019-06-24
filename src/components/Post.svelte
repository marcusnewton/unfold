<script context="module">
  export const p_gql = `
    title
    date
    body
  `;
</script>

<script>
  export let data;
</script>

<div class="box">
  <h1 class="title">{data.title}</h1>
  <h2 class="subtitle">{data.date}</h2>
  <div class="block">{data.body}</div>
</div>
