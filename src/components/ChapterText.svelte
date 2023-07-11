<script>
    import { getContext } from "svelte";
    const copy = getContext("copy");
</script>

<div class="prose">
    {#each copy.lookBack as text, i}
    <p>{@html text.value}</p>
    {/each}
</div>

<style>
    .prose {
        width: 100%;
        display: flex;
        justify-content: center;
        flex-direction: column;
        max-width: 60rem;
        margin: 0 5rem;
        line-height: 2;
        height: 100vh;
        overflow-y: hidden;
    }
</style>