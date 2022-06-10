<script lang="ts">
  import Home from '@/pages/Home.svelte'
  import Header from '@/components/Header.svelte'
</script>

<main>
  <Header/>

  <Home/>
</main>

<style lang="scss">
  :root {
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen,
      Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
    height: 100%;
  }
  :global(body) {
    margin: 0;
    height: 100%;
    background-color: #fbfbfb;
  }
</style>
