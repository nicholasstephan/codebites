<script context="module">
  export async function load({params, fetch}) {
    const url = `https://datadatadata.online/rest/codebites/bites/${params.id}`;
    let response = await fetch(url);
    return {
      status: response.status,
      props: {
        data: response.ok && (await response.json())
      }
    };
  }
</script>

<script>
  export let data;
</script>

{@html data.code}
