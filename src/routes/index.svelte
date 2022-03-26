<script context="module">

  export async function load({_, fetch}) {
    const url = `https://datadatadata.online/rest/codebites/bites`;
    let response = await fetch(url);
    return {
      status: response.status,
      props: {
        bites: response.ok && (await response.json())
      }
    };
  }

</script>

<script>

  export let bites = [];

  console.log(bites);

</script>

<header>
  <h1>&lt;CODE/&gt;</h1>
</header>

<article>
  {#each bites as bite}
    <a href="/{bite.id}">{bite.title}</a>
  {/each}

</article>


<style>

  header {
    box-sizing: border-box;
    height: 600px;
    display: flex;
    align-items: center;
    justify-content: center;
  }

  h1 {
    font-size: 80px;
    font-family: 'Roboto Mono', monospace;
  }

  article {
    max-width: 800px;
    margin: 0 auto;
  }

  article a {
    display: block;
    color: white;
    text-decoration: none;
    padding: 4px 0;
  }
  
</style>