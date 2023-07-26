<script>
	import { getContext, onMount } from "svelte";
	import Header from "$components/Header.svelte";
	import Intro from "$components/Intro.svelte";
	import ScrollText from "$components/ScrollText.svelte";
	import Chapter from "$components/Chapter.svelte";
	import BarChart from "$components/BarChart.svelte";
	import Wall from "$components/Wall.svelte";
	// import Footer from "$components/Footer.svelte";

	// const copy = getContext("copy");
	// const data = getContext("data");
	let scrollY = 0;
	let containerElement;
	let w;

	import data from "$data/listings.csv";
    import * as d3 from "d3";

	let raunchinessData = data.filter(d => d.cover_url.includes("http")).filter(d => d["Man partially unclothed"] == "true" || d["Woman partially unclothed"] == "true").sort((a, b) => d3.ascending(a["Year Season"], b["Year Season"]));
	let illustrationData = data.filter(d => d.cover_url.includes("http")).filter(d => d.Style == "Illustrated").sort((a, b) => d3.ascending(a["Year Season"], b["Year Season"]));
	let raceData = data.filter(d => d.cover_url.includes("http")).filter(d => d["Has POC"] == "true").sort((a, b) => d3.ascending(a["Year Season"], b["Year Season"]));

	console.log(raunchinessData, illustrationData, raceData);

	//on mouse wheel 
	function onScroll(e) {
		if (scrollY >= 0) {
			scrollY+=e.deltaY;
		} else {
			scrollY = 0
		}
	}
</script>

<svelte:window bind:scrollY={scrollY} />

<!-- <Header /> -->
<div on:mousewheel={onScroll}
	bind:this={containerElement}
	bind:clientWidth={w}
	class="scrollContainer"
	style="transform: translateX(-{scrollY}px);
	width:{w}px">
	<Wall data={raunchinessData} />
</div>
<ScrollText />
<BarChart data={raunchinessData} />

<style>
	.scrollContainer {
		width: 100%;
		position: fixed;
		height: 100vh;
	}
</style>
