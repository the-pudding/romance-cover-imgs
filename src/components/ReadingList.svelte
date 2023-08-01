<script>
    import { readingList } from "$stores/misc.js";
    import Icon from "$components/helpers/Icon.svelte";
    export let data;

    console.log(data);

    function findBookMatch(id, type) {
        let match = data.find(d => d.ISBN == id);

        if (type == "title") { return match.title }
        else if (type == "img") { return match.ISBN }
    }
</script>

<section id="reading-list">
    <div class="paper">
        <h3>Your Reading List</h3>
        {#if $readingList.length > 1}
            <ul>
                {#each $readingList as book, i}
                <li>
                    <img src ="/assets/images/img_{findBookMatch(book.id, "img")}.jpg" alt="a thumbnail book cover of {findBookMatch(book.id, "title")}">
                    <div class="details">
                        <p class="title">{findBookMatch(book.id, "title")}</p>
                        <p class="author">By Author Name</p>
                    </div>
                    <button class="remove"><Icon name="x" /></button>
                </li>
                {/each}
            </ul>
        {:else}
            <p>Click on the + signs next to each book to add them to your list</p>
        {/if}
    </div>
</section>

<style>
    #reading-list {
        width: 100%;
        height: 100vh;
        position: fixed;
        left: 0;
        top: 0;
        background: rgba(255, 255, 255, 0.95);
        backdrop-filter: blur(2px);
        z-index: 999;
    }
    .paper {
        background: white;
        max-width: 50rem;
        transform: translateX(-50%);
        width: 100%;
        height: 80vh;
        margin: 0 auto;
        position: absolute;
        left: 50%;
        bottom: 0;
        box-shadow: -0.25rem 0 1rem  var(--color-gray-100);
        padding: 2rem;
    }
    h3 {
        font-family: 'Canela';
        text-align: center;
        font-size: var(--36px);
    }
    ul {
        margin-top: 5rem;
    }
    li {
        display: flex;
        flex-direction: row;
        border-bottom: 1px solid var(--color-gray-100);
        padding: 1rem;
        justify-content: space-between;
        align-items: center;
    }
    .details {
        width: calc(100% - 5rem);
    }
    .title {
        font-family: 'Canela';
        font-size: var(--24px);
        padding: 0;
        margin: 0;
    }
    .author {
        font-family: var(--sans);
        padding: 0;
        margin: 0;
    }
    li img {
        width: 3rem;
        object-fit: contain;
        margin-right: 2rem;
    }
    li button {
        width: 3rem;
        height: 3rem;
        border-radius: 50%;
        background: var(--romance-pink);
    }
    :global(li button svg line) {
        stroke: white;
    }
</style>