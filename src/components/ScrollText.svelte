<script>
    import { getContext } from "svelte";
    import { fade } from 'svelte/transition';
    import { fly } from 'svelte/transition';
    import { highlightYear } from "$stores/misc.js";
    const copy = getContext("copy"); 
    
    export let scrollY;
    $: console.log(scrollY)
    let scrollIndex = 1;

    $: visible = scrollY > 200;
</script>

<div id="scroll-text">
    {#each copy.raunchinessScroll as text, i}
        {#if $highlightYear == text.triggerYear}
            <p in:fly={{ y: 50, duration: 1000 }} out:fade>{@html text.text}</p>
        {/if}
    {/each}
</div>

<style>
    #scroll-text {
        position: fixed;
        top: 2rem;
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