<script lang="ts">
    // pages
    import Home from '@/pages/Home.svelte'

    // components
    import Note from '@/components/Note.svelte'
    import Header from '@/components/Header.svelte'
</script>

<main>
    <Header/>
    <Note
        id={1234}
        title={'Some note'}
        content={'This note is about this that'}
        tags={['Test', 'Text']}
        date={'20220610000'}
        isFavorite={false}
    />
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
</style>
