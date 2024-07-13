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
        width: 100%;
        text-align: center;
        background-color: white;
        border: 1px solid black;
        display: table;
    }

    button:hover {
        background-color: red;
    }
</style>
