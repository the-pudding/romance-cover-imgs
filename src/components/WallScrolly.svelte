<script>
	import Scrolly from "$components/helpers/Scrolly.svelte";
    import Wall from "$components/Wall.svelte";
    import { getContext } from "svelte";
	let value;
    export let data;
    export let copy;
	export let section;
</script>

<section id="scrolly">
	<div class="sticky">
        <Wall data={data} value={value} section={section}/>
    </div>
	<Scrolly bind:value>
        {#if copy}
            {#each copy as text, i}
                <div class="step">
                    <p>{text.text}</p>
                </div>
            {/each}
        {/if}
	</Scrolly>
	<div class="spacer" />
</section>

<style>
	.sticky {
		position: sticky;
		top: 3rem;
		transition: all 1s;
		height: 100vh;
        z-index: 1;
        overflow-x: hidden;
	}

	.spacer {
		height: 75vh;
	}

	.step {
		height: 80vh;
		text-align: center;
        z-index: 999;
        max-width: 30rem;
        margin: 0 auto;
	}

	.step p {
		padding: 1rem;
        text-align: left;
        padding: 2rem;
        background: var(--color-white);
	}
</style>
