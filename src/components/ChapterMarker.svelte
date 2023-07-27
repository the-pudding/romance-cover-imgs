<script>
    import { activeSection } from "$stores/misc.js";

    const sections = ["raunchiness", "illustration", "race"]
</script>

<nav>
    {#each sections as section, i}
        {@const active = $activeSection == section ? "active" : ""}
        <button class="sectionBox {active}" id="sectionBox-{section}"></button>
    {/each}
</nav>

<style>
    nav {
        width: 100%;
        position: fixed;
        top: 0rem;
        padding: 1rem 0 0 0;
        display: flex;
        flex-direction: row;
        justify-content: center;
        align-items: center;
        z-index: 1000;
        height: 3rem;
        background: linear-gradient(rgba(255, 249, 249, 1), rgba(255, 249, 249, 0.75), rgba(255, 249, 249, 0))
    }

    .sectionBox {
        width: 20px;
        height: 20px;
        background: rgb(247, 193, 181, 0.5);
        margin: 0 1rem;
        border: 3px solid #F7C1B5;
        opacity: 0.5;
        transition: 0.25s ease-in-out;
    }
    .sectionBox.active {
        opacity: 1;
    }
    .sectionBox:hover {
        opacity: 1; 
    }
</style>