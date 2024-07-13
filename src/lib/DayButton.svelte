<script>
    import { createEventDispatcher } from "svelte";
    const dispatch = createEventDispatcher();
    export let day;
    let btn_str = day.getDate();
    let clicked = false;

    function clicked_day() {
        clicked = !clicked;
        dispatch("day_clicked", { day });
    }
</script>

<main>
    <button class:clicked on:click={clicked_day}>{btn_str}</button>
</main>

<style>
    main {
        display: flex;
        justify-content: center;
    }

    .clicked {
        background-color: red;
    }

    button {
        width: 80%;
        text-align: center;
        background-color: #242424;
        margin: 3px;
    }

    button:hover {
        background-color: red;
    }
</style>
