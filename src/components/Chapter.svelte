<script>
    import Wall from "$components/Wall.svelte";
    import ChapterText from "$components/ChapterText.svelte";
    let w;

    export let data;
</script>

<svelte:window bind:innerWidth={w} />

<section>
    <!-- <ChapterText /> -->
    <Wall data={data}/>
</section>

<style>
    section {
        display: flex;
        flex-direction: row;
    }
</style>