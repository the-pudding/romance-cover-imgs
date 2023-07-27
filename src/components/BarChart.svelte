<script>
    import * as d3 from "d3";
    import { onMount } from "svelte";
    import { highlightYear } from "$stores/misc.js";
    import { fade, fly } from 'svelte/transition';

    export let data;
    let w;

    let barChartW;
    $: console.log(data);
    $: groupedData = d3.groups(data, d => d.year);
</script>

<svelte:window bind:innerWidth={w} />

<section id="barChart">
    <p class="label left">2011</p>
    <div class="chart-wrapper" bind:clientWidth={barChartW}>
        {#each groupedData as year, i}
            {@const isHighlightYear = $highlightYear == year[0] ? "highlightYear" : ""}
            <div class="year-bar {isHighlightYear}" 
            style="height: {year[1].length*1.5}px;
            width: {barChartW/groupedData.length}px"
            >
                {#if $highlightYear == year[0]}
                    <p class="count count-{isHighlightYear}"
                    in:fly={{ y: 20, duration: 500 }} out:fade>
                        {year[1].length}
                    </p>
                {/if}
            </div>
        {/each}
    </div>
    <p class="label right">2023</p>
</section>

<style>
    #barChart {
        position: fixed;
        width: 100%;
        height: 10rem;
        left: 0;
        bottom: 0;
        display: flex;
        flex-direction: row;
        justify-content: center;
        z-index: 1000;
        background: linear-gradient(rgba(255, 249, 249, 0), rgba(255, 249, 249, 0.75), rgba(255, 249, 249, 1))
    }
    .chart-wrapper {
        display: flex;
        flex-direction: row; 
        align-items: end;
        height: 100%;
        width: 60%;
        position: relative;
    }
    .year-bar {
        width: 5rem;
        background: #F7C1B5;
        margin: 0 0.05rem;
        transition: 0.25s ease-in;
        position: relative;
    }
    .highlightYear {
        background: blue;
    }
    .count {
        margin: 0;
        padding: 0;
        position: absolute;
        width: 100%;
        text-align: center;
        top: -1.5rem;
        transition: 0.25s ease-in;
        opacity: 0;
    }
    .count-highlightYear {
        opacity: 1;
    }
    .label {
        margin: 0;
        padding: 0;
        display: flex;
        align-self: flex-end;
        font-family: "Canela";
        color: #F7C1B5;
        opacity: 30%;
        font-size: 36px;
        padding: 0;
        line-height: 1;
    }
    .label.left {
        margin: 0 1rem 0 0;
    }
    .label.right {
        margin: 0 0 0 1rem;
    }
</style>
