<script>
    import { createEventDispatcher } from "svelte";
    const dispatch = createEventDispatcher();
    export let day;
    export let hour;
    export let selected;

    function clicked_tile_time() {
        dispatch("tile_times_clicked", { day, hour });
    }
    function mouse_down_from_here() {
        dispatch("mouse_down_from_here", { day, hour });
    }
    function mouse_over_to_here() {
        dispatch("mouse_over_to_here", { day, hour });
    }
</script>

<main>
    <button
        class:selected
        on:click={clicked_tile_time}
        on:mousedown={mouse_down_from_here}
        on:mouseover={mouse_over_to_here}
        on:focus={}
        class="tile_time"
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

    .selected {
        background-color: red;
    }

    .tile_time:hover {
        background-color: red;
    }
</style>
