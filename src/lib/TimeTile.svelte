<script>
    import { createEventDispatcher } from "svelte";
    const dispatch = createEventDispatcher();
    export let day;
    export let hour;
    let day_hour = [day, hour];
    let clicked = false;

    function clicked_tile_time() {
        clicked = !clicked;
        dispatch("tile_times_clicked", { day_hour });
    }
</script>

<main>
    <button class:clicked on:click={clicked_tile_time} class="tile_time"
    ></button>
</main>

<style>
    .tile_time {
        width: 60px;
        height: 22px;
        background-color: white;
        border: 1px solid black;
        display: table;
    }

    .clicked {
        background-color: red;
    }

    .tile_time:hover {
        background-color: red;
    }
</style>
