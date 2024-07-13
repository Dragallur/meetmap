<script>
    import DayButton from "./DayButton.svelte";
    let days_of_week = ["", "Sun", "Mon", "Tue", "Wed", "Thu", "Fri", "Sat"];
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
    let n_weeks = 5;
    let arr_days = [];
    let arr_months = [];
    let day = new Date();
    let day_of_week = day.getDay();

    day.setDate(day.getDate() - day_of_week);
    for (let i = -day_of_week; i < n_weeks * 7 - day_of_week; i++) {
        arr_days.push(new Date(day));
        let foo = new Date(day);
        foo.setDate(day.getDate() + 7);
        if (day.getDate() > foo.getDate()) {
            arr_months.push(
                months[day.getMonth()] + "/" + months[foo.getMonth()],
            );
        } else {
            arr_months.push(months[day.getMonth()]);
        }
        day.setDate(day.getDate() + 1);
    }
</script>

<main>
    <div class="grid-container">
        {#each days_of_week as day}
            <div class="grid-day-names">{day}</div>
        {/each}
        {#each arr_days as day, i}
            {#if i % 7 === 0}
                <div class="grid-month-name">{arr_months[i]}</div>
            {/if}
            <DayButton {day} on:day_clicked />
        {/each}
    </div>
</main>

<style>
    .grid-container {
        display: grid;
        grid-template-columns: repeat(8, 1fr);
        background-color: black;
        border: 2px solid #ff0000;
        align-items: center;
        margin: 5px;
        padding: 10px;
    }

    .grid-month-name {
        white-space: nowrap;
        color: #ff0000;
        font-weight: bold;
        font-size: 14px;
        margin-right: 2px;
    }

    .grid-day-names,
    .grid-month-name {
        text-align: center;
        color: #ffffff;
        font-size: 12px;
    }

    .grid-day-names {
        font-weight: bold;
        text-transform: uppercase;
        color: #cccccc;
    }
</style>
