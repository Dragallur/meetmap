<script>
    import { createEventDispatcher } from "svelte";
    const dispatch = createEventDispatcher();
    export let day;
    export let hour;
    export let selected;

    function select_from_here() {
        dispatch("select_from_here", { day, hour });
    }
    function select_to_here() {
        dispatch("select_to_here", { day, hour });
    }
    function mouse_up() {
        dispatch("mouse_up", { day, hour });
    }
</script>

<main>
    <button
        class:selected
        on:mousedown={select_from_here}
        on:mouseover={select_to_here}
        on:focus={select_to_here}
        on:mouseup={mouse_up}
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
        background-color: rgb(255, 76, 76);
    }
</style>
