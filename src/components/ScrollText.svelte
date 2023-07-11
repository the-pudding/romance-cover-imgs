<script>
    import { getContext } from "svelte";
    import { fade } from 'svelte/transition';
    import { fly } from 'svelte/transition';
    const copy = getContext("copy"); 
    
    export let scrollY;
    $: console.log(scrollY)
    let scrollIndex = 1;

    $: visible = scrollY > 200;
</script>

<div id="scroll-text">
    {#each copy.lookBack as text, i}
        {#if scrollIndex == i && visible}
            <p in:fly={{ y: 50, duration: 1000 }} out:fade>{@html text.value}</p>
        {/if}
    {/each}
</div>

<style>
    #scroll-text {
        position: fixed;
        top: 5rem;
        width: 100%;
        display: flex;
        justify-content: center;
    }

    #scroll-text p {
        max-width: 35rem;
        font-size: 14px;
        line-height: 1.65;
    }
</style>