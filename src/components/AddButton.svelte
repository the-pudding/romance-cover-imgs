<script>
    import Icon from "$components/helpers/Icon.svelte";
    import { fly } from 'svelte/transition';
    import { readingList, highlightYear } from "$stores/misc.js";
    import * as d3 from "d3";

    let showMessage = false;

    function handleBtnClick(e) {
        let btn = d3.select(this);
        let textFeedback = btn.select(".message");

        let bookID = e.target.parentNode.parentNode.id;
            if (bookID == "") {
                bookID = e.target.parentNode.parentNode.parentNode.id;
            }
            if (bookID.includes("chunk")) {
                bookID = e.target.parentNode.parentNode.id; 
            }
        bookID = bookID.split("_")[1];

        if ((this.className).includes("book_inList")) {
            btn.classed("book_inList", false);
            btn.classed("book_noList", true); 
            const indexOfObject = $readingList.findIndex(object => { return object.id == bookID })
            $readingList.splice(indexOfObject, 1)
            textFeedback.text("Book removed!")
            showMessage = true;
        } else {
            btn.classed("book_inList", true)
            btn.classed("book_noList", false); 
            $readingList = [...$readingList, { id: bookID }];
            textFeedback.text("Book added!")
            showMessage = true;
        }  

        setTimeout(() => {
            showMessage = false;
        }, 3000);
    }
</script>

<button 
    on:click={handleBtnClick}
    class="add book_noList">
    <Icon name="plus" />
    <p class="message" class:visible={showMessage}>Book added!</p>
</button>

<style>
    .add {
        position: absolute;
        bottom: -0.75rem;
        right: -0.75rem;
        border-radius: 50%;
        display: flex;
        align-items: center;
        justify-content: center;
        height: 1.5rem;
        width: 1.5rem;
        background-color: var(--color-gray-900);
        border: 2px solid white;
        box-shadow: 0.25rem 0 1rem  var(--color-gray-300);
        transition: 0.25s transform linear, 0.5s background-color linear;
    }
    :global(.add.book_inList) {
        background-color: var(--romance-pink);
        transition: 0.5s background-color linear;
    }
    :global(.add svg) {
        margin-top: 0.25rem;
        pointer-events: none;
    }
    :global(.add.book_noList svg) {
        transform: rotate(0deg);
        /* background-color: var(--color-gray-900);
        transition: 0.25s rotate linear-out, 1s background-color 0.25s; */
    }
    :global(.add.book_inList svg) {
        transform: rotate(45deg);
        transition: 0.25s rotate linear;
    }
    :global(.add svg line) {
        stroke: white;
        pointer-events: none;
    }
    .message {
        position: absolute;
        font-size: var(--12px);
        font-weight: 700;
        opacity: 0;
        top: 50%;
		left: 50%;
        transform: translate(-50%, -100%);
        transition: 0.125s all linear;
        background-color: white;
        border-radius: 0.25rem;
        padding: 0.25rem;
        box-shadow: 1rem 0 1rem  var(--color-gray-100);
    }
    .message.visible {
		opacity: 1;
		transform: translate(-50%, -200%);
	}
</style>