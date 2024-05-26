<script>
    export let arr_clicked_days = [];
    let months = [
        "Jan",
        "Feb",
        "Mar",
        "Apr",
        "May",
        "Jun",
        "Jul",
        "Aug",
        "Sep",
        "Oct",
        "Nov",
        "Dec",
    ];
    let min_time = 7;
    let max_time = 16;

    function create_time_label(index) {
        let time_label = String(index / 2 + min_time).padStart(2, "0") + ":00";
        return time_label;
    }
</script>

<main>
    <div class="timetable">
        <div class="time_column">
            {#each Array((max_time - min_time) * 2 + 1) as _, i}
                <div class="time_label">
                    {#if i % 2 === 0}
                        {create_time_label(i)}
                    {/if}
                </div>
            {/each}
        </div>
        <div class="schedule">
            {#each arr_clicked_days as day}
                <div class="schedule_days">
                    {months[day.getMonth()] + " " + day.getDate()}
                    <div class="tile">
                        {#each Array((max_time - min_time) * 2) as _, i}
                            <div class="tile_time"></div>
                        {/each}
                    </div>
                </div>
            {/each}
        </div>
    </div>
</main>

<style>
    .timetable {
        display: flex;
        border: 2px solid;
        background-color: black;
        margin: 5px;
    }

    .time_column {
        display: flex;
        flex-direction: column;
        margin: 5px;
        margin-top: 18px;
        margin-right: 1px;
    }

    .time_label {
        display: flex;
        justify-content: center;
        align-items: center;
        border: 1px solid transparent;
        height: 20px;
        color: gray;
    }

    .schedule {
        display: flex;
        background-color: black;
        overflow-x: scroll visible;
        white-space: nowrap;
        margin: 5px;
        margin-left: 0px;
    }

    .schedule_days {
        text-align: center;
    }

    .tile_time {
        width: 60px;
        height: 20px;
        background-color: white;
        border: 1px solid black;
    }
</style>
