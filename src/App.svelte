<script lang="ts">
    // pages
    import Home from '@/pages/Home.svelte'

    // components
    import Header from '@/components/Header.svelte'
</script>

<Header/>
<main>
    <Home/>
</main>

<style lang="scss">
    :root {
        font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen,Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
        height: 100%;
    }
    :global(body) {
        margin: 0;
        height: 100%;
        background-color: #fbfbfb;
    }
    main {
        padding: 2em;
        margin: 0 auto;
        width: 100vw;
        box-sizing: border-box;
    }
</style>
