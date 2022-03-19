<script context="module">

  export async function load({params, fetch}) {
    const url = `https://datadatadata.online/rest/codebites/bites/${params.id}`;
    let response = await fetch(url);
    return {
      status: response.status,
      props: {
        demoUrl: `/demo/${params.id}`,
        data: response.ok && (await response.json())
      }
    };
  }

</script>

<script>

  import Prism from 'prismjs';

  export let data;
  export let demoUrl;

  $: code = Prism.highlight(data['sample-code'], Prism.languages.markup, 'markup');

  let scrollTop = 0;
  $: headerOpacity = Math.min( Math.max(0.9 - scrollTop/400, 0), 1) + 0.1;

</script>


<svelte:window bind:scrollY={scrollTop}/>

<header style="background-image:url({data.cover}); opacity:{headerOpacity};"/>

<section>
  <h1>{data.title}</h1>
  <article>{@html data.article}</article>
  <div class="code-wrap">
    <code>{@html code}</code>
  </div>
  <a href="{demoUrl}" class="demo button" target="_blank">See it in action.</a>
</section>


<style>

  header {
    position: sticky;
    top: 0;
    width: 100vw;
    height: 400px;
    background-size: cover;
    background-position: center;
  }

  header:before {
    content: "";
    position: absolute;
    left: 0;
    top: 0;
    right: 0;
    height: 20%;
    z-index: 10;
    background: linear-gradient(to top, rgba(var(--background-rgb),0) 0%, rgba(var(--background-rgb),1) 100%);
  }

  header:after {
    content: "";
    position: absolute;
    left: 0;
    bottom: 0;
    right: 0;
    height: 40%;
    z-index: 10;
    background: linear-gradient(to bottom, rgba(var(--background-rgb),0) 0%, rgba(var(--background-rgb),1) 100%);
  }

  section {
    position: relative;
    z-index: 20;
    width: calc(100vw - 32px);
    max-width: 800px;
    padding: 0 0 80px 0;
    margin: -100px auto 0;
  }

  h1 {
    margin-left: -3px;
    font-size: 60px;
    line-height: 64px;
    color: var(--forground);
  }

  article {
    position: relative;
    margin: 0 0 32px 0;

    font-size: 18px;
    line-height: 24px;
    color: var(--comments);
  }

  article:before {
    position: absolute;
    top: -56px;
    left: -72px;
    
    content: "<!--";
    font-size: 64px;
    line-height: 64px;
    font-weight: bold;
    letter-spacing: -10px;
    color: var(--comments);
    opacity: 0.2;
  }

  article:after {
    position: absolute;
    right: -24px;
    bottom: -40px;
    
    content: "-->";
    font-size: 64px;
    line-height: 64px;
    font-weight: bold;
    letter-spacing: -10px;
    color: var(--comments);
    opacity: 0.1;
  }

  article :global(em),
  article :global(i) {
    color: var(--green);
  }

  article :global(strong),
  article :global(b) {
    color: var(--orange);
  }

  .code-wrap {
    width: 100%;
    overflow-y: hidden;
    overflow-x: auto;
    margin-bottom: 40px;
  }

  .demo.button {
    color: var(--forground);
  }

</style>