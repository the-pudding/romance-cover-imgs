<script>
    import * as d3 from "d3";
    import { onMount } from "svelte";
    import { highlightYear } from "$stores/misc.js";

    export let data;

    let cleanedData = data.filter(d => d.cover_url.includes("http")).filter(d => d["Man partially unclothed"] == "true" || d["Woman partially unclothed"] == "true").sort((a, b) => d3.ascending(a.year, b.year));
    let groupedData = d3.groups(cleanedData, d => d.year);
    let w;

    let barChartW
    console.log(groupedData);
</script>

<svelte:window bind:innerWidth={w} />

<section id="barChart">
    <p class="label left">2011</p>
    <div class="chart-wrapper" bind:clientWidth={barChartW}>
        {#each groupedData as year, i}
            {@const isHighlightYear = $highlightYear == year[0].split("-")[0] ? "highlightYear" : ""}
            <div class="year-bar {isHighlightYear}" 
            style="height: {year[1].length/35*100}px;
            width: {barChartW/groupedData.length}px"
            ></div>
        {/each}
    </div>
    <p class="label right">2023</p>
</section>

<style>
    #barChart {
        position: fixed;
        width: 100%;
        height: 20rem;
        left: 0;
        bottom: 0;
        display: flex;
        flex-direction: row;
        justify-content: center;
    }
    .chart-wrapper {
        display: flex;
        flex-direction: row; 
        align-items: end;
        height: 100%;
        width: 60%;
    }
    .year-bar {
        width: 5rem;
        background: #F7C1B5;
        margin: 0 0.05rem;
        transition: 0.25s ease-in;
    }
    .highlightYear {
        background: blue;
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
