<script>
    import Wall from "$components/Wall.svelte";

    import data from "$data/listings.csv";
    import * as d3 from "d3";

	let raunchinessData = data.filter(d => d.cover_url.includes("http")).filter(d => d["Man partially unclothed"] == "true" || d["Woman partially unclothed"] == "true").sort((a, b) => d3.ascending(a["Year Season"], b["Year Season"]));
	let illustrationData = data.filter(d => d.cover_url.includes("http")).filter(d => d.Style == "Illustrated").sort((a, b) => d3.ascending(a["Year Season"], b["Year Season"]));
	let raceData = data.filter(d => d.cover_url.includes("http")).filter(d => d["Has POC"] == "true").sort((a, b) => d3.ascending(a["Year Season"], b["Year Season"]));

	console.log(raunchinessData, illustrationData, raceData)

    let scrollY = 0;
	let containerElement;
	let w;

    //on mouse wheel 
	function onScroll(e) {
		if (scrollY >= 0) {
			scrollY+=e.deltaY;
		} else {
			scrollY = 0
		}
	}
    $: console.log(scrollY, w)
</script>

<!-- <div on:mousewheel={onScroll}
	bind:this={containerElement}
	bind:clientWidth={w}
	class="horiz" 
	style="transform: translateX(-{scrollY}px);
		width:{w}px">
    <Wall data={raunchinessData} />
</div> -->

<Wall data={raunchinessData} />

<style>
    .horiz {
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100vh;
    }
</style>