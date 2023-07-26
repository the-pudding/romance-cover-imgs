<script>
	import "$styles/app.css";

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

<main on:mousewheel={onScroll}
	bind:this={containerElement}
	bind:clientWidth={w}
	id="content" 
	class="horiz" 
	style="transform: translateX(-{scrollY}px)">
	<slot />
</main>

<style>
	main {
		width: auto;
		height: 100vh;
	}
</style>
